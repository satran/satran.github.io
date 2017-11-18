---
layout: post
title: Implementing tail's follow in Go
summary:
---

`tail` is a command most of us are familiar with. And I would assume you are also familiar with the `-f` option that it exposes. And to those that aren't familiar it prints out the last few lines of a file. Recently working on a project I wondered what I need to do to implement this on my own. The thought comes from reading Feynman's book[1]:

> No doubt you know how to do it; but when you play with this sort of problem as a kid, and you haven't been shown the answer... it's fun trying to figure out how to do it. Then, as you go into adulthood, you develop a certain confidence that you can discover things; but if they've already been discovered, that you shouldn't bother you at all. What one fool can do, so can another, and the fact that some other fool beat you to it shouldn't disturb you: you should get a kick out of having discovered something.

It probably is a trivial thing to implement. But I thought it would be a good start to a series of articles in which I write how something is implemented. So let me take you through my process of trying to figure out how to implement `tail -f` in Go.

First, let's understand the problem. The tail command provides a flag which you can "follow" a file with. What it does is waits for any changes that are added to the end of the file and prints it for you. For simplicity I'm not going to implement tail, rather just the follow function. So we print the whole file at the beginning and then print lines as they are added. 

My first take of it was the very naive way of doing it. Print all the bytes in the file till we reach an `io.EOF`; let the process sleep for a second and then try reading again. Let's look at the function:

```go
func follow(file io.Reader) error {
	r := bufio.NewReader(file)
	for {
		by, err := r.ReadBytes('\n')
		if err != nil && err != io.EOF{
			return err
		}
		fmt.Printf(string(by))
		if err == io.EOF {
			time.Sleep(time.Second)
		}
	}
}

```

It sadly doesn't react promptly when content is written to the file. Linux provides an API to monitor file system events: the inotify AP. The man pages give you a good introduction. It provides two functions that interest us: `inotify_init` and `inotify_add_watch`. The `inotify_init` function creates an object which we would use for further interaction with the API. The `inotify_add_watch` function allows you to specify the events of files you are interested in. There are several events that the API emits, but we are concerned with the `IN_MODIFY` event, emitted when a file is modified.

Since we are using Go we will have to stick to the `syscall` package. It provides wrappers for the functionality mentioned earlier: `syscall.InotifyInit` and `syscall.InotifyAddWatch`. Using syscall let's see how we can implement the follow function. I have omitted error handling for brevity, where you see an `_` variable being used it is a good place to handle the error returned.

```
func follow(filename string) error {
	file, _ := os.Open(filename)
	fd, _ := syscall.InotifyInit()
	_, _ := syscall.InotifyAddWatch(fd, filename, syscall.IN_MODIFY)
	r := bufio.NewReader(file)
	for {
		by, err := r.ReadBytes('\n')
		if err != nil && err != io.EOF {
			return err
		}
		fmt.Printf(string(by))
		if err != io.EOF {
			continue
		}
		if err = waitForChange(fd); err != nil {
			return err
		}
	}
}

func waitForChange(fd int) error {
	for {
		var buf [syscall.SizeofInotifyEvent]byte
		_, _ := syscall.Read(fd, buf[:])
		if err != nil {
			return err
		}
		r := bytes.NewReader(buf[:])
		var ev = syscall.InotifyEvent{}
		_ = binary.Read(r, binary.LittleEndian, &ev)
		if ev.Mask&syscall.IN_MODIFY == syscall.IN_MODIFY {
			return nil
		}
	}
}
```

The `InotifyInit` function returns a file handler that can be used to read `sycall.InotifyEvent`s. Reading from this handler is a blocking operation. This allows us to react only when the event is created.

If you were to handle multiple operating systems it would be better to handle this more generically. This is where the `fsnotify` package comes in. It provides an abstraction over inotify for Linux, kqueue for BSD etc. Using the fsnotify our function looks very similar to the earlier one but much simpler.

```go
func follow(filename string) error {
	file, _ := os.Open(filename)
	watcher, _ := fsnotify.NewWatcher()
	defer watcher.Close()
	_ = watcher.Add(filename)

	r := bufio.NewReader(file)
	for {
		by, err := r.ReadBytes('\n')
		if err != nil && err != io.EOF {
			return err
		}
		fmt.Printf(string(by))
		if err != io.EOF {
			continue
		}
		if err = waitForChange(watcher); err != nil {
			return err
		}
	}
}

func waitForChange(w *fsnotify.Watcher) error {
	for {
		select {
		case event := <-w.Events:
			if event.Op&fsnotify.Write == fsnotify.Write {
				return nil
			}
		case err := <-w.Errors:
			return err
		}
	}
}
```

I hope the code explains better than the text I have written. I have omitted several cases where the code could fail for brevity. For a sound implementation of the functionality I would have to dig deeper. But this was good enough for me to quence the thirst of knowing how it works. I hope it did the same for you too.

[1] [Feynman Lectures on Computation](http://amzn.to/2AIWVuX)

