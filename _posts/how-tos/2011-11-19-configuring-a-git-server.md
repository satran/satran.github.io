---
layout: post
title: Configuring a Git Server
---
# [{{ page.title }}]({{ page.url }})

There are many ways to set up a Git server. In this article I am going to show you how you can do it using the SSH protocol. First I am assuming you have a UNIX or GNU/Linux machine with you. I am not very sure if this works well on windows, I am assuming it would. 

####**Installing basic packages on the server**
You must have ssh installed in your machine and the daemon must be running. On [Fedora](http://fedoraproject.org) it comes in by default, while on [Ubuntu](http://ubuntu.com) you have to install the `openssh-server` package. On a Mac the service is disabled by default. Go to System Preferences -> Sharing and enable Remote Login. 

Now that you have `sshd` enabled we can proceed to setting up the git server. You must have git installed in the machine, get the instructions for your machine [here](http://git-scm.com/download). For the rest of the document I am going to call the server `r2d2` and the client machine `gandalf`. 
<!-- more -->
####**Creating the Repository**
It is best to have a dedicated user for the git repository. I have created a user called `git` in `r2d2` and have placed my repositories inside the directory `~git/repositories`. Either you can copy an existing repository or create a new one. I will show you both. To create a new repository `hello_world` run this command in the repository directory.

    git --init bare hello_world.git

To copy an existing repository, assuming the repository is in /var/ftp/hello_world, run

    git clone --bare /var/ftp/hello_world hello_world.git

Now that you have the repository create let me show you how to access it.

####**Accessing the Repository**
On the client `gandalf` I need to create a ssh key pair. My user on `gandalf` is `satyajit`. To create the ssh key pair I run this command:

    ssh-keygen

You will see an output similar to this

    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/satyajit/.ssh/id_rsa): 
    Created directory '/home/satyajit/.ssh'.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/satyajit/.ssh/id_rsa.
    Your public key has been saved in /home/satyajit/.ssh/id_rsa.pub.
    The key fingerprint is:
    83:77:da:13:a9:da:26:eb:dd:7b:9a:35:59:ff:50:cd satyajit@r2d2
    The key's randomart image is:
    +--[ RSA 2048]----+
    |                 |
    |                 |
    |                 |
    |       .   .   ..|
    |      . S +   . E|
    |       . * . o o |
    |        o o + . .|
    |      .+.. +.. ..|
    |     .++o =+    .|
    +-----------------+

This will create two files `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`. The `id_rsa.pub` is your public key. Copy this file into the server `r2d2`. Lets say I copied it to `~git/keys` as `satyajit.pub`. To give access to the git user add the key `satyajit.pub` to the `authorized_keys`.

    cat ~/keys/satyajit.pub >> ~/.ssh/authorized_keys

This will copy your public key to the `authorized keys` in the server. Doing this allows access to the server via ssh using the git user, without having to type in the git's password. 

To clone the repository hello_world, from your client `gandalf` run:

    git clone git@192.168.1.1:~git/repositories/hello_world.git

Please note I have used the server's IP address here, you can replace it with the host name of your server. Since git has read and write permission on the repositories folder you can push the data too. 

If you want to share the repository with other users just copy their public keys and append them to the authorized_keys file.

Further if you want to prevent shell access to the system using the user `git` edit the /etc/passwd file:

    sudo vim /etc/passwd

At the bottom of the file you will find the `git` user's configuration:

    git:x:1003:10003::/home/git:/bin/sh

Just replace the `/bin/sh` to `/usr/bin/git-shell` as shown below:

    git:x:1003:10003::/home/git:/usr/bin/git-shell

Now if you try accessing ssh using the user `git` you will get a response similar to 

    ssh git@192.168.1.1
    fatal: What do you think I am? A shell?
    Connection to gitserver closed.

####**Notes**
Please keep in mind this is definitely not the best method to use in a public network. It is suitable for a small team in a local network. When you have many users copying and managing all the public keys will become a task by itself. Stay tuned for another article on how to do that.


