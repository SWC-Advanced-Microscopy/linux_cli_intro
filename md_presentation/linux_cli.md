---
theme: ./assets/dark.json
author: Rob Campbell
date: MMMM dd, YYYY
paging: Slide %d / %d
---


```
~~~bash
figlet -k -w 125 -c  "The   Linux   CLI" 
jp2a --width=20 --colors ./assets/tux.jpg | sed -e 's/^/                                                     /'
~~~
```
```
~~~bash
figlet -k -w 125 -c "a   practical   guide"
~~~
```

## All info at:
* Browser to: [https://tinyurl.com/linuxCLIintro](https://tinyurl.com/linuxCLIintro)
* Or: `git clone https://tinyurl.com/linuxCLIintroGit`

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
* You type commands at the prompt and they are processed immediately. 

```bash
rob@juicer:~/Dropbox (UCL)/work/Presentations/Linux_CLI_Intro$ ls -l
total 8
drwxrwxr-x 3 rob rob 4096 Apr 19 12:51 md_presentation
-rw-rw-r-- 1 rob rob 1913 Apr 19 13:20 README.md

```
---





# Why bother with this stuff? This isn't the `80s. 

* The CLI commands are often very powerful and highly customizable. 
* They can be chained together to very simply build "one line programs". 
* You can execute your own Python functions at the command line and they will integrate seamlessly. 
* The Linux (e.g. bash/zsh) CLIs are now cross-platform and much nicer than the Windows terminal.
* Almost all commands you will see today have many more features than we have time to cover.
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
Make a big file:

```bash
$ ls -lkh /usr/bin > BINFILES
 ```
* then try the following.
`cat`, `head`, `tail`, `less`


## Editing text files
* Do not edit text file in a word processor!
* `nano` (The geeky options are `emacs` and `vim`)
* Let's edit BINFILES in `nano` then view it with `head`


## CAUTIONS
* Avoid spaces in filenames because they are annoying. 
* In fact, avoid most funny characters: `&`, `*`, `/`, `\`, quotes, brackets, `|`
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

Cool!
Making connections is now faster **and** you can automate tasks.

For example, print the system log file of the remote machine without needing to enter a password:
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk 'dmesg'
```

## Teleporting through bastion to juicer automatically
It is possible to perform the hop from bastion to juicer transparently.
See the Notes.md file for an example. 
---












# Persistent terminals
Q. SSH sessions die when you log off or are disconnected, so how to initiate things that may run for extended periods? 

A. `tmux`!

* Starting `tmux`
* Renaming sessions with `ctrl-b` then `$` 
* Leaving the session with `ctrl-b` then `d`
* Listing available sessions. 
* Reattaching to the same session: `tmux ls` and `tmux attach -t SESSION_NAME`
* Multiple panes. Vertical: `ctrl-b` and `%` ; Horizontal: `ctrl-b` and `"`
* Moving between panes with `ctrl-b` and an arrow key
* Killing the session
---



# Persistent terminals
Q. SSH sessions die when you log off or are disconnected, so how to initiate things that may run for extended periods? 

A. `tmux`!

* Starting `tmux`
* Renaming sessions with `ctrl-b` then `$` 
* Leaving the session with `ctrl-b` then `d`
* Listing available sessions. 
* Reattaching to the same session: `tmux ls` and `tmux attach -t SESSION_NAME`
* Multiple panes. Vertical: `ctrl-b` and `%` ; Horizontal: `ctrl-b` and `"`
* Moving between panes with `ctrl-b` and an arrow key
* Killing the session

## We can get help at the command line!
`man tmux`

---



# Persistent terminals
Q. SSH sessions die when you log off or are disconnected, so how to initiate things that may run for extended periods? 

A. `tmux`!

* Starting `tmux`
* Renaming sessions with `ctrl-b` then `$` 
* Leaving the session with `ctrl-b` then `d`
* Listing available sessions. 
* Reattaching to the same session: `tmux ls` and `tmux attach -t SESSION_NAME`
* Multiple panes. Vertical: `ctrl-b` and `%` ; Horizontal: `ctrl-b` and `"`
* Moving between panes with `ctrl-b` and an arrow key
* Killing the session

## We can get help at the command line!
`man tmux`

## Let's put it all together
* Log on to `juicer`
* Create a `tmux` session and name it. 
* Open a terminal with two panes. 
* We will put an editor in one pane and run the code in the other.
* We will cover the most basic way of creating a Python script and running it at the CLI. 
But the point of the exercise is mainly to get happy navigating around a `tmux` terminal.

---








# Copying, moving, and deleting

## Making new directories
* `mkdir somedir`
* `mkdir -p directoryOne/nestedDirectory2`

## Moving/renaming/deleting files
* Copying with `cp`
* Moving and renaming at the same thing: `mv`
* Wildcards
* Deleting with `rm` and `rmdir`
* Deleting LOTS of stuff `rm -frv`


## CAUTIONS
* Deleting files is forever
---





# Using rsync to copy
## Copying and compressing
* The wonders of `rsync`. 
* The trailing `/`
* `rsync` over `ssh`
* `rsync -av data.zip /mnt/winstor`
---




# Compressing and archiving
The **t**ape **ar**chive command, `tar`, can be used to compress:

```
tar -czv -f ARCHIVE_NAME.tar.bz /folder/to/compress
```
* This will **c**reate an archive that is g**z**ip compressed and be **v**erbose. 
* It will create the archive **f**ile "ARCHIVE_NAME.tar.bz" and will put into it the path defined in the final argument.

gzip compression is fairly slow. 
If you have lots of files you can compress in parallel (using all cores) using parallel bzip:
```
tar -I lbzip2 -cv -f ARCHIVE_NAME.tar.bz /folder/to/compress
```
---





# Searching for files and text 
Let's use searching for files and text as an example for how we can chain commands together. 
We will use BrainSaw acquisition logs on PC joiner as a test case:


```
$ cd /mnt/data/BakingTrayStacks/ADMIN/acquisitionStats
$ ls -l akrami/anatomy/virus_tests/VP_CAP01
```

Find find all the "recipe" files and count them we will know how many samples were acquired with a pipe.
```
$ find . -name '*recipe*'
$ find . -name '*recipe*' | wc -l
```

This is how we list only the file names and sort them alphabetically:
```
$ find . -name '*recipe*' -printf '%f\n' | sort | less
```

How many of those file names are unique?
```
$ find . -name '*recipe*' -printf '%f\n' | sort | wc -l
$ find . -name '*recipe*' -printf '%f\n' | sort | uniq | wc -l
```

Count the number of lines in each file:

```
$ find . -name '*recipe*' -exec wc -l {} \;
```

We can go crazy and find the number of lines in these files and how often this occurs:
```
find . -name '*recipe*'  -type f -exec wc -l {} \;  | sed 's/ .*//' | sort | uniq -c
```
---




# Searching for text
We can use `grep` to search for text.
Users generally add their initials to the recipe. 
How do we find all of the recipes from Nicole Vissers?

```
$ find . -name '*recipe*' | grep 'NV_' | wc -l
71
```

We can count up the number OrganGrinder vs NeuroVision acquisitions.
The system ID is in the recipe file. e.g.
```
$ tail sjones/users/fred/Data_brainsaw/FM_mar226/recipe_FM_mar226_210109_124650.yml
```
so:
```
find . -name '*recipe*' -type f -exec grep 'ID: OrganGrinder' {} \; | wc -l
find . -name '*recipe*' -type f -exec grep 'ID: neurovision' {} \;  | wc -l
```
You can do similar things to easily return stuff like the number of unique TIFF sizes in a directory.



## These operations can work on remote content too!
```bash
curl -s http://brainsaw.mouse.vision/ | grep 'Sample'
```
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





# Where to go from here?
* Job control with `fg` and `bg`. Placing tasks into the background with `&`
* Learn about configuring your shell by editing `.bashrc` (see example in repo)
* Learn Emacs keybindings (Mac OS uses them all over the place too)
* Consider switching to `zsh` and trying PowerLevel10k
* Learn the basics of shell scripts (BASH scripts). Or just ask ChapGPT...
