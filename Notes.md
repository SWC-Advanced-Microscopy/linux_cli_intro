# Notes

These notes provide examples and context to go along with the Linux CLI presentation. 
It is a plain text file decorated with [markdown syntax](https://en.wikipedia.org/wiki/Markdown). 
It will look pretty viewed on GitHub or in editors such as [Typora](https://typora.io/).




# Finding your way around
## Directory structures
The file system is a tree of nested directories. 
The final common node is known as "root" (`/`). 
You can list all directories that are nested right under root with:

```bash
$ ls /
```
**NOTE**: the `$` denotes the command line (BASH) prompt and you do not type it in.

The `~` denotes the user's (your own) "home" directory, where you keep private files. 
We can do:

```bash
$ ls ~
```

`ls` is a command. 
It has so-called "switches" to modify its behavior.
e.g. "long" output with `-l`

```bash
$ ls -l ~
❯ # time passses
total 212
drwx------  2 rob rob   4096 Sep  2  2021  AnyDesk
-rw-rw-r--  1 rob rob 103554 May 26  2022  BaslerDemo.ipynb
drwxrwxr-x  6 rob rob   4096 Apr 19 12:51  bin
drwxrwxr-x  7 rob rob   4096 Aug 18  2022  brainregister
-rw-rw-r--  1 rob rob    113 Jan 24 11:07  ceph.txt
drwxr-xr-x  2 rob rob   4096 Nov 29 15:28  Desktop
-rw-rw-r--  1 rob rob   4164 Apr 24 09:55  dircolors.default
drwxr-xr-x  3 rob rob   4096 May 21  2022  Documents
drwxr-xr-x  9 rob rob  12288 Apr 24 14:47  Downloads
drwx------ 12 rob rob   4096 Apr  7  2022  Dropbox
...
```

The first block of stuff (`drwxr-xr-x`) are permissions (who can read, write, or execute). 
Then we have info on who owns the files (`rob`). 
Then the size in bytes. 
Then when the file was last modified. 
Finally the name. 

How do we know what switches `ls` will accept? 
You can ask!
To get help you can use the `man` command. e.g.

```
man ls
```

You can return the name of the current directory with `pwd` (print working directory)

```bash
$ pwd
```

and  `ls` with no directory input argument lists the contents:
```bash
$ ls
```


You can change directory with `cd`.
e.g.

```bash
$ cd /etc
```

Folders and files that start with a `.` are hidden by default. 
The `-a` (all) switch to `ls` will show them. 
Compare `ls ~` to `ls -a ~`. 
You can combine switches: `ls -la ~`

## Auto-complete and wild cards
Try typing `ls` then press tab. 
All directories in the current directory are display to help you complete. 
Linux has a `/etc` directory that houses config files. 
If you type `ls /e` then tab, the directory name will complete. 

The `*` matches anything. Running `ls -d ~/.*` will list all hidden files in your home folder.

---


# Basic CLI commands

## Creating files
The `touch` command will either make a new file with that name or update the last modified file time of a file. 

```
$ touch TEST
$ ls -l TEST
-rw-rw-r-- 1 rob rob 0 Apr 24 15:14 TEST
```
Time passes...

```
$ touch TEST
$ ls -l TEST
-rw-rw-r-- 1 rob rob 0 Apr 24 15:22 TEST
```

* redirect output to a file. e.g. `ls -l /usr/ >> test` and `ls -l /usr/ > test`

## Viewing the contents of text files
Make a big file then try the following
* `cat`, `head`, `tail`, `less`

## Editing text files
* Do not edit text file in a word processor?
* `nano` (The geeky options are `emacs` and `vim`)
* Let's edit our file in `nano` then view it. 


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
Q. SSH sessions die when you log off or are disconnected, so how to initiate things that may run for extended periods? 

A. `tmux`!

* Starting `tmux`.
* Renaming sessions with `ctrl-b` then `$` 
* Leaving the session with `ctrl-b` then `d`
* Listing available sessions. 
* Reattaching to the same session: `tmux ls` and `tmux attach -t SESSION_NAME`
* Multiple panes. Vertical: `ctrl-b` and `%` ; Horizontal: `ctrl-b` and `"`
* Moving between panes with `ctrl-b` and an arrow key
* Killing the session. 

## We can get help at the command line!
`man tmux`

## Let's put it all together
* Log on to `juicer`
* Create a `tmux` session and name it. 
* Open a terminal with two panes. Run MATLAB in one and edit a script in the other.
* Run the script.
* Leave the session and kill it. `tmux kill-session -t SESSION_NAME`
---








# Copying, moving, and deleting

## Making new directories
* `mkdir somedir`
* `mkdir -p directoryOne/nestedDirectory2`

## Moving/renaming/deleting files
* Copying with `cp`
* Deleting with `rm` and `rmdir`
* Deleting LOTS of stuff `rm -frv`
* Moving and renaming at the same thing: `mv`
* Wildcards

## CAUTIONS
* Deleting files is forever
---





# Using rsync to copy (and compress)
## Copying and compressing
* The wonders of `rsync`. 
* `rsync` over `ssh`
* Compressing files using parallel algorithms: `tar` and `lbzip2`. Demo.

```bash
tar -I lbzip2 -cvf ARCHIVE_NAME.tar.bz /folder/to/compress
```
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
* Learn the basics of shell scripts (BASH scripts)
* Consider switching to `zsh` and trying PowerLevel10k
