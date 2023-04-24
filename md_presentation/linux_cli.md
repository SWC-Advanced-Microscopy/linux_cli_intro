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





# What is a command line?

* The Linux command prompt will typically end with a `$` and may be colored.
* You can also run interactive MATLAB, Python, and R sessions within the terminal.
* MATLAB running in the command line always has a `>>` prompt.
* Simple job control:

```bash
rob@juicer:~/Dropbox (UCL)/work/Presentations/Linux_CLI_Intro$ ls -l
total 8
drwxrwxr-x 3 rob rob 4096 Apr 19 12:51 md_presentation
-rw-rw-r-- 1 rob rob 1913 Apr 19 13:20 README.md

```
---






# Finding your way around
* Directory structures. Root (`/`) and home (`~`)
* Navigating directories with `ls`, `pwd`, `cd` 
* Switches: `ls` vs `ls -l`
* Hidden folder and files (`.`) and `ls -a`
* Wildcards: `*`
* Tab for auto-completes
---



# Finding your way around
* Directory structures. Root (`/`) and home (`~`)
* Navigating directories with `ls`, `pwd`, `cd` 
* Switches: `ls` vs `ls -l`
* Hidden folder and files (`.`) and `ls -a`
* Wildcards: `*`
* Tab for auto-completes


## Help!
To get help you can use the `man` command. e.g.

```
man ls
```
---





# Basic CLI commands

## Creating files
* `touch`
* redirect output to a file. e.g. `ls -l /usr/ >> test` and `ls -l /usr/ > test`

## Viewing the contents of text files
Make a big file then try the following
* `cat`, `head`, `tail`, `less`

## Editing text files
* `nano` (The big editors, `vim` and `emacs`, we skip)
* Let's edit our file in `nano` then view it. 


## CAUTIONS
* Spaces in filenames
* Funny characters
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












# Persistent terminals
SSH sessions die when you log off or are disconnected, so how to initiate things that may run for extended periods?
* How to work with persistent terminals using `tmux`. What is tmux? 
* Starting `tmux`, reattaching to the same session. Renaming sessions.
* Multiple panes. 
* Listing available sessions. 
* Killing the session. 

## Let's put it all together
* Log on to `juicer`
* Open a terminal with two panes. Run MATLAB in one and edit a script in the other.
* Run the script.
---










# Basic CLI commands

## Moving/renaming/deleting files
* `mv`, `rm`, `cp`, `mkdir`

## Copying and compressing
* The wonders of `rsync`. 
* `rsync` over `ssh`
* Compressing files using parallel algorithms: `tar` and `lbzip2`. Demo.



## CAUTIONS
* Deleting files is forever
---





# Searching for files and text 
* Finding files with `find`. 
* `uniq` and `sort`
* Doing things with the find command: `-exec` flag. 
* **Piping** to other commands to, for example, count files (`wc`). 

Go over some fancier examples, like how to find all the unique TIFF sizes in a directory.
Searching for directories vs files. Search for files by size. 
Using `grep` to search many files for specific text strings. Lots of examples showing useful CLI switches. 
Finding files. Including fancier stuff like how to find all the unique file sizes in a directory.
Example:





# These operations can work on remote content too!
```bash
curl -s http://brainsaw.mouse.vision/ | grep 'Sample'
```

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

## GUI vs CLI
Avoid the GUI file managers if possible. `rsync` over the terminal is better.


## Common Mistakes
* `ls` to mount point directories that do not exit. 
* Thinking that an unmounted directory is connected to the server.
---





# Where to go from here?
* Job control with `fg` and `bg`
* Learn about configuring your shell by editing `.bashrc` (see example in repo)
* Learn Emacs keybindings (Mac OS uses them all over the place too)
* Learn the basics of shell scripts 
* Consider switching to `zsh` and trying PowerLevel10k
