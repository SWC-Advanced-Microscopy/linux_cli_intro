---
theme: ./assets/dark.json
author: Rob Campbell
date: MMMM dd, YYYY
paging: Slide %d / %d
---





```


```
```
~~~bash
figlet -k -w 125 -c  "The   Linux   CLI" 
jp2a --colors ./assets/tux.jpg | sed -e 's/^/                                            /'
~~~
```
```
~~~bash
figlet -k -w 125 -c "a   practical   guide"
~~~
```
---






# Make sure you have installed everything

## On Mac
```
brew install rsync lbzip2 htop nload nano vim ncdu curl wget telnet
```

## On Linux
```
apt install rsync lbzip2 htop nload nano vim ncdu curl wget telnet
```

```



```

```
~~~cowsay
Let us begin!
~~~
```
---





# What Is Linux?
* From where and when did it come? 

```
~~~bash
jp2a --colors --width=120 ./assets/sun_logo.jpg
~~~
```
---



# What Is Linux?
* From where and when did it come? 
* GNU. 

```
~~~bash
jp2a --colors --width=62 ./assets/gnu.jpg
~~~
```
---



# What Is Linux?
* From where and when did it come? 
* GNU/Linux. 

```
~~~bash
jp2a --colors --width=120 ./assets/gnu_linux.jpg
~~~
```
---




# What Is Linux?
* From where and when did it come? 
* GNU/Linux. 
* What is a "distribution"?

```
~~~bash
jp2a --colors --width=70 ./assets/ubuntu.jpg
~~~
```
---




# What Is Linux?
* From where and when did it come? 
* GNU/Linux. 
* What is a "distribution"?
* What is a desktop environment?

```
~~~bash
jp2a --colors --width=60 ./assets/kde.jpg
~~~
```
---




# What Is Linux?
* From where and when did it come? 
* GNU/Linux. 
* What is a "distribution"?
* What is a desktop environment?
* What is the command line?

```bash
rob@juicer:~/Dropbox (UCL)/work/Presentations/Linux_CLI_Intro$ ls -l
total 8
drwxrwxr-x 3 rob rob 4096 Apr 19 12:51 md_presentation
-rw-rw-r-- 1 rob rob 1913 Apr 19 13:20 README.md

```
---






## A very quick example
* The command prompt (make sure it's not MATLAB! `$` not `>>`)
* Directory structures. Root (`/`) and home (`~`)
* Navigating directories with `ls`, `pwd`, `cd` 
* Switches: `ls` vs `ls -l`
* Hidden folder and files (`.`) and `ls -a`
* Wildcards: `*`
* Tab for auto-completes
---






# Secure Shell: SSH
* Logging onto remote machines with SSH. 

```
ssh USERNAME@ssh.swc.ucl.ac.uk
```

* Then hop on to a desktop PC with another SSH command. e.g.
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

* VPN allows you to bypass the first hop.
---



# Secure Shell: SSH
* Logging onto remote machines with SSH. 

```
ssh USERNAME@ssh.swc.ucl.ac.uk
```

* Then hop on to a desktop PC with another SSH command. e.g.
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

* VPN allows you to bypass the first hop.


## SSH without passwords
* Authenticating using a shared key instead of a password. 
* Generate a shared key with `ssh-keygen`. Press return when asked to enter a pass-phrase. 
* Now we will send this to a remote machine. e.g.
```
ssh-copy-id USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

* You can test it:
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```
---



# Secure Shell: SSH
* Logging onto remote machines with SSH. 

```
ssh USERNAME@ssh.swc.ucl.ac.uk
```

* Then hop on to a desktop PC with another SSH command. e.g.
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

* VPN allows you to bypass the first hop.


## SSH without passwords
* Authenticating using a shared key instead of a password. 
* Generate a shared key with `ssh-keygen`. Press return when asked to enter a pass-phrase. 
* Now we will send this to a remote machine. e.g.
```
ssh-copy-id USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

* You can test it:
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

## Why bother?
As well as making manual connections faster, this means you can automate tasks. For example, print the system log file of the remote machine without needing to enter a password:
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk 'dmesg'
```
---






# Basic CLI commands

## Help!
You have already seen `ls`, `pwd`, and `cd` and can tab to auto-complete. 
To get help you can use the `man` command. e.g.

```
man ls
```
---



# Basic CLI commands

## Creating files
* `touch`
* nano/vim/emacs (just what they are in less than 5 minutes). How to quit from `vi` and `emacs`!
* redirect output (`>`, `>>`)
* Pipes

## CAUTIONS
* Spaces in filenames
* Funny characters
---



# Basic CLI commands

## Moving/renaming/deleting files
    * `mv`, `rm`, `cp`, `mkdir`

## CAUTIONS
* Deleting files is forever
---



# Basic CLI commands

## Displaying/printing file contents
* `echo`, `cat`, `less`, `head`, `tail` (or `cat ~/.ssh/config | cowsay`)
* `uniq` and `sort`

## Scripting
* Bash scripts exist but are beyond the scope of the course.
---





# Status of your system
* Disk space with `df`
* `ncdu` (`ctrl-c` to break out of long-running commands)
* System status with `htop` (or `top`)
---





# What are mount points?
Mount points are just like Windows shares: they are directories that point to something else.
For example, a mounted server.
You will see mount points with `df`.
[SSH to `juicer` and try]. 

## Common Mistakes
* `ls` to mount point directories that do not exit. 
* Thinking that an unmounted directory is connected to the server.
---




# Searching for files and text 
* Finding files with `find`. 
* Doing things with the find command: `-exec` flag. 
* Piping to other commands to, for example, count files (`wc`). 

Go over some fancier examples, like how to find all the unique TIFF sizes in a directory.
Searching for directories vs files. Search for files by size. 
Using `grep` to search many files for specific text strings. Lots of examples showing useful CLI switches. 
Finding files. Including fancier stuff like how to find all the unique file sizes in a directory.
Example:

```bash
curl -s http://brainsaw.mouse.vision/ | grep 'Sample'
```
---





# Copying and compressing
* How to copy files using `cp` and `rsync`. 
* Avoid the GUI file managers. 
* Compressing files using parallel algorithms: `tar` and `lbzip2`. Demo.



# Persistent terminals
* How to work with persistent terminals using `tmux`. What is tmux? 
* Starting `tmux`, reattaching to the same session. Renaming sessions.
* Multiple panes. 
* Listing available sessions. 
* Killing the session. 

