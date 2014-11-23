---
layout: post
title: Go best practises
summary: I have been building the back-end for Endles, a product we make at Studio March, primarily in Go. There have been a few pleasant surprises that the language provides. Here I try to explain an opinionated best practises while coding in Go.
---


I have been building the back-end for [Endless](http://studiomarch.com/endless/), a product we make at Studio March, primarily in Go. There have been a few pleasant surprises that the language provides. Here I try to explain an opinionated best practises while coding in Go.


## Use the standard library.

Always see if there is something in the standard library that fits your need before looking else where. In most cases the standard library is just enough.

##### The flag package for most configurations.
The `flag` package is  seen as parsing arguments from the command line. It can also be used to store configurations your code might need. It also helps serve documentation for all the configurations.

    var port int
    flag.IntVar(&port, "port", 8000, "Specifies the port the server listens to.")

This can either be used as command line arguments or in places which needs default values.

##### The database/sql as a substitute for the many ORMs
I searched for days to stick to an ORM but finally decided to stick with the vanilla `database/sql` package. Many might think this takes us back a step but its simplicity makes up for any drawback. ORMs generally take the least common set of features a database provides. For example you cannot take advantages that Postgres give you with Hstore or Array data types. With the `database/sql` you can.

##### I use the net/http
For my needs the `net/http` fits  well for the few end points of the API. Sometimes I use the [Gorilla tool kit](http://gorillatoolkit.org/) when the `http` package is not enough. More than a full fledge framework use what you need from the `net/http` package or the toolkit.

##### others
The `log` package does most of your logging at ease. It is also thread safe which means you can have global `Logger`s to do all your logging. Use the `log.Lshortfile` flag for debugging purposes. The `testing` suite with the `go test` command is enough for most test cases.


## Use the tools provided with go

Go provides tools like `gofmt` `go test` which ease up your development, use them effectively.

##### gofmt
If you have programmed with Go before you will know that the language designers decided to put a full stop in styling discussions with the `gofmt` tool. The tool decides how many tabs, spaces between parenthesis and all the non-essential discussions. But you might have missed the wonderful option which can be used to re-factor your code. The `-r` option just does that. 

    gofmt -r 'pattern -> replacement' <files>
    
Thus if you want to change a struct Program to Process you would

    gofmt -r 'Program -> Process' -w .
    
If you just want to list the files that contain the changes use a `-l`. Use `godoc gofmt` to learn more.


##### go test
The test suite of go has a lot of gems hidden. I use the `-test.run=TestFunction` many times. The tool also provides coverage and benchmark analysis. The several tools go provides are useful and enough for most cases. Do read the documentation of these tools. I'm sure you will find some that surprise you. 

## Organize your Go code
The Go language internally uses a format which we can follow nearly. Go files that expose a `main` package, that is one that builds an executable, reside inside `cmd` folder and libraries inside `pkg` folder. We can use the `cmd` folder to store executables and the root folder(we don't need to use the `pkg` folder to simplify import paths). So if we were creating a web server we could do something like this:

    cmd/
        endless/
                main.go
                api.go
                ...
    models.go
    db.go
    ...
    
This way in our endless/main.go we can use an import path like `github.com/endless/models` etc.


## And a few others

##### Use environment variables for sensitive information
Use the `os.Getenv("VARIABLE_NAME")` to set passwords and other sensitive in your program. This way you avoid pushing passwords in your versioning system.

##### Use your $HOME folder for $GOPATH
This is just convenience. Setting it will automatically put binaries in `$HOME/bin` and navigating through code can be easier by just following `$HOME/src`.

##### Naming conventions
Follow standards in [Effective Go](https://golang.org/doc/effective_go.html#names) for naming conventions. Try to make your packages read like `users.New` or `sessions.DB`.

##### Keep it simple
The beauty of Go is its simplicity, so try to do the same with your code. Avoid exposing too many variables/structs/functions. Make your API small and simple. This makes it easier to maintain your code.


As I keep coding in Go I learn something new every day. This is definitely not an exhaustive list and some of it is opinionated, take it with a pinch of salt. One good advice is to try the idiomatic way of Go. Almost always the designers have got it right. 
    