# Notes

These notes provide examples and context to go along with the Linux CLI presentation. 
It is a plain text file decorated with [markdown syntax](https://en.wikipedia.org/wiki/Markdown). 
It will look pretty viewed on GitHub or in editors such as [Typora](https://typora.io/).




# Finding your way around
## Directory structures
The file system is a tree of nested directories. 
The common common node at the base of the tree is known as "root" (`/`). 
You can view all directories right under root with the **l**i**s**t command:

```
$ ls /
```
**NOTE**: the `$` denotes the command line (e.g. bash or zsh) prompt and you do not type it in.

The `~` symbol denotes your own "home" directory, where you keep private files. 
We can list this in the same way:

```
$ ls ~
```

`ls` is a command. 
It has so-called "switches" to modify its behavior.
e.g. "long" output with `-l`

```
$ ls -l ~

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
The single number that follows is the number of directories linked to it. 
Then we have info on who owns the files (`rob`) and what user group they belong to (`rob`). 
Then the size in bytes. 
Then when the file was last modified. 
Finally the name. 

The **man**ual command will tell us what switches `ls` will accept and how it works:

```
$ man ls
```

You can return the name of the current directory with `pwd` (**p**rint **w**orking **d**irectory)

```
$ pwd
```

and  `ls` with no directory input argument lists the contents of the current directory:
```
$ ls
```


You can change directory with `cd`.
e.g.

```
$ cd /etc
```

The symbol `.` means current directory and `..` means one directory up. 
So to go up one directory you can:

```
$ cd ../
```

## Hidden files and combining switches
* Folders and files that start with a `.` are hidden by default. 
* The `-a` (all) switch to `ls` will show hidden files.
* Compare `ls ~` to `ls -a ~`. 
* You can combine switches: `ls -la ~`

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

## Redirecting "standard ouput"
All the stuff that's been appearing on the command line is what is known as "standard output."
We can redirect this to a file with the `>` and `>>` operators.
The `>` will empty the file before filling it. 
The `>>` will append if the file already exists. 
e.g.

```
$ ls -l /usr/ > test
$ cat test
$ ls -l /usr/ >> test
$ cat test
$ ls -l /usr/ > test
$ cat test
```


## Viewing the contents of text files
Make a big file:

```
$ ls -lkh /usr/bin > BINFILES
```

Let's see what's in it. 
The first 10 lines:
```
$ head BINFILES                                                      
total 82176                                                          
-rwxr-xr-x   1 root   wheel   231K 11 Aug  2022 AssetCacheLocatorUtil
-rwxr-xr-x   1 root   wheel   288K 11 Aug  2022 AssetCacheManagerUtil
-rwxr-xr-x   1 root   wheel   229K 11 Aug  2022 AssetCacheTetheratorUtil
-rwxr-xr-x  76 root   wheel   163K 11 Aug  2022 DeRez
-rwxr-xr-x  76 root   wheel   163K 11 Aug  2022 GetFileInfo
-rwxr-xr-x   1 root   wheel   234K 11 Aug  2022 IOAccelMemory
-rwxr-xr-x   1 root   wheel   108K 11 Aug  2022 IOMFB_FDR_Loader
-rwxr-xr-x  76 root   wheel   163K 11 Aug  2022 ResMerger
-rwxr-xr-x  76 root   wheel   163K 11 Aug  2022 Rez
```
The first 3 lines:
```
$ head -n 3 BINFILES                                                      
total 82176                                                          
-rwxr-xr-x   1 root   wheel   231K 11 Aug  2022 AssetCacheLocatorUtil
-rwxr-xr-x   1 root   wheel   288K 11 Aug  2022 AssetCacheManagerUtil
```

`tail` does the same thing but for the end of the file
```
$ tail -2 BINFILES                                      
-rwxr-xr-x   1 root   wheel   3.2K 11 Aug  2022 znew  
-rwxr-xr-x   1 root   wheel   198K 11 Aug  2022 zprint
```

The `cat` command dumps everything to the screen, so if the file is long you only see the last screenful. 
The `less` command lets you scroll through slowly.


## Editing text files
* Do not edit text files in a word processor: create and save as plain text.
* Try `nano` for editing at the CLI at first. If you find yourself doing this a lot, the geeky power-tools options are `emacs` and `vim`. 
* You can use an external editor like [SublimeText](https://www.sublimetext.com/) or [Pulsar](https://pulsar-edit.dev/), but this is tricky to do when you logged in to a PC remotely.


## CAUTIONS
* Avoid spaces in filenames because they are annoying. 
* In fact, avoid most funny characters: `&`, `*`, `/`, `\`, quotes, brackets, `|`
---




# Secure Shell: SSH
The command line makes a lot of sense when you want to log onto a machine remotely and you can't or don't want to set up virtual desktop. 
If you have good command line knowledge you can do almost anything without a GUI. 
That includes things like installing software from the internet, checking disk and CPU usage, and starting analyses in MATLAB or Python. 
We will be logging onto machines remotely using the secure shell: SSH. 
Here, a *client* machine (the one your are sitting at) logs on to a remote machine: the *server*. 
This is achieved using the `ssh` command, your remote user name, and the remote PC name. 
We can log on to the SWC gateway server (a bastion server) as follows:

```
ssh USERNAME@ssh.swc.ucl.ac.uk
```

We can then hop to any PC on the network with another SSH command. e.g.

```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

If you are on Eduroam you must do the two hops to get to the desktop PC. 
If you are on the SWC's VPN or on ethernet you to bypass the first hop.


## SSH without passwords
You have to type in your password each time with SSH and this can be annoying if you SSH often or if you want to automate tasks via SSH. 
Now we will try authenticating without a password using a shared key instead: 
* First we generate a shared key with `ssh-keygen`. Press return when asked to enter a pass-phrase. 
* Now we will send this to a remote machine. e.g.
```
ssh-copy-id USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

To test it, try to SSH to the machine. 
You will see you don't need a password if it worked. 
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk
```

The way this works is that the server encrypts a known message with the public key we sent it. 
If the client (us) can read the message and report it back then the server accepts that we have the key and lets us on.
We decrypt using private key which nobody else has access to. 

## Why bother?
As well as making manual connections faster, this means you can automate tasks. For example, print the system log file of the remote machine without needing to enter a password:
```
ssh USERNAME@juicer.mrsic-flogel.swc.ucl.ac.uk 'dmesg'
```

## Getting to `juicer` via the bastion without having to do the two hops manually. 
It's annoying to have to perform two SSH commands and bastion does not accept shared keys.
We can, however, hop through bastion to juicer automatically.
First make the file `~/.ssh/config` if it is not already there. 
Then add to it:

```
Host bastion
    Hostname ssh.swc.ucl.ac.uk
    User robc

Host juicer
    Hostname juicer.mrsic-flogel.swc.ucl.ac.uk
    User YOUR_USER_NAME
    ProxyJump bastion
```

Obviously edit the string `YOUR_USER_NAME` to reflect your actual user name on the system.
Now you can:
```
$ ssh YOUR_USER_NAME@juicer
```
and all you have to do is type in your bastion password. 
You will be automatically teleported to `juicer`.

---





# Persistent terminals
SSH is very useful but if you close the window running the server or are otherwise disconnected, all your work vanishes.
This may not matter if you are just typing in commands, but if you are running a file compression or analysis it will be stopped.
Luckily there is a solution: `tmux` the terminal multiplexer. 

The `tmux` command gives you a persistent terminal that will only die if the PC reboots or you stop it.
It is really worth getting to know this program but it require learning a few keyboard shortcuts. 
You will forget them at first but they are listed at the [tmux cheatsheet](https://tmuxcheatsheet.com/). 
Here we will cover only the basics. 

## Starting
You start the program at the command line by running `tmux`. 
This creates a new, blank, `tmux` session. 

## Rename and leaving the session
The key combination `ctrl` and `b` pressed together (`ctrl-b`) puts `tmux` into command mode. 
It interprets the next as a command. 
Two useful commands to learn first are:

* Renaming sessions with `ctrl-b` then `$` then enter a new name and press return.
* **D**isconnecting from the session (so it can be resumed) with `ctrl-b` then `d`

## Listing sessions and re-connecting
If you have left your `tmux` session and dormant sessions running, you can list them:
```
$ tmux ls
AMAZING_SESSION: 1 windows (created Mon Apr 24 20:05:38 2023)
rob: 1 windows (created Mon Apr 24 18:58:12 2023)
```
We can reconnect to session "rob":
```
$ tmux attach -t rob
```

## Breaking up a session into separate panels
You can have multiple command lines in one session. 
That is why it's a terminal **multiplexer**.
You can split things up vertically: `ctrl-b` and `%` or  horizontally: `ctrl-b` and `"`.
Then you move between panes with `ctrl-b` and an arrow key

## Killing the session
Either type `exit` from within `tmux` or from outside the running session:

```
$ tmux ls
AMAZING_SESSION: 1 windows (created Mon Apr 24 20:05:38 2023)
rob: 1 windows (created Mon Apr 24 18:58:12 2023)

(base) rob@mbp[Downloads]$ tmux kill-session -t AMA

(base) rob@mbp[Downloads]$ tmux ls
rob: 1 windows (created Mon Apr 24 18:58:12 2023)
```

Note how we do not have to type the whole name out: just enough to make sure it's uniquely identifiable. 
In this case the first letter alone would have sufficed. 


## We can get help at the command line!
`man tmux`

## Let's put it all together
* Log on to a remote machine.
* Create a `tmux` session and name it. 
* Open a terminal with two panes. 
* In the first pane we will `touch myFile.py` then `nano myFile.py` (the extension is for convention only).
* Add Python code that will run. e.g. `print('Hello I am an egg')`
* In the other pane run `python ./myFile.py`
* Now we will get rid of need to type "python" into the prompt. 

Your Python interpreter can be found as follows:
```
$ which python
/Users/rob/mambaforge/bin/python
```

So we modify the script to have it read:
```
#!/Users/rob/mambaforge/bin/python
print('Hello I am an egg')
```
Note the `#!` (hash-bang). 
This tells the CLI to interpret the file using the program that comes after on that line. 
Make the script "executable" using `chmod`: the `+x` adds execute permissions. 
```
$ chmod +x myFile.py
$ ls -l ./myScript.py
-rwxr-xr-x  1 rob  staff  53 24 Apr 18:34 ./myScript.py
(base) rob@mbp[Downloads]$ ./myScript.py
Hello I am an egg
```

---








# Copying, moving, and deleting

## Making new directories
* To make one directory in the current directory: `mkdir somedir`
* To make one directory in some other path: `mkdir /home/username/scripts/somedir`
* To make a new directory (`directoryOne`) and nest another new directory within it: `mkdir -p directoryOne/nestedDirectory2`

## Moving/renaming/deleting files
### Copying
You can copy single or multiple files with `cp`.
Make a copy of `myPythonCode.py` in `./data/analysis`
```
$ cp myPythonCode.py ./data/analysis
```
Make copies of three `.py` files:
```
$ cp interp2d.py interp3d.py batch.py ./data/analysis
```

Files can be moved, rather than copied, in the same way. 
Just use the `mv` command instead:
```
$ mv interp2d.py interp3d.py batch.py ./data/analysis
```
i.e. this will copy and delete

You can move or copy *all* `.py` file using the `*` wildcard:
```
$ mv *.py ./data/analysis
```

### Deleting files
You can delete files with `rm` and empty folders `rmdir`:
```
$ rm my_file
$ rm my_folder
```

Delete all `.py` files:
```
$ rm *.py
```

To delete all files in a folder and the folder's contents:
```
$ rm -frv ./MY_FOLDER 
```
This **f**orces the removal **r**ecursively and is **v**erbose (prints what it does to CLI).


**CAUTION** -- Deleting files is forever! There is no trash. 

---





# Using rsync to copy
The `rsync` command is like a very clever version of `cp`. 
It is designed for archiving or transferring large quantities of files. 
You can use it to copy files from A to B then later re-run the same command and only copy over the changes.
Typical usage:
```
$ rsync -av ./source/ /some/other/destination/
```

**NOTE** If the source directory ends with a trailing `/` then the *contents* are copied. 
So the above copies the contents of `source`. 
If if want to copy `source` and its contents we would do:

```
$ rsync -av ./source /some/other/destination/
```

You can do this over ssh:
```
$ rsync -av ./source USER@juicer:/home/USER/Downloads/
```

Of course if you have a server mounted at, say, `/mnt/winstor` then we can copy data to the server by doing:
```
$ rsync -av data.zip /mnt/winstor
```

Of course if you have a remote server mounted 



## Making archives with tar
We will not go into the **t**ape **ar**chive command, `tar` in much detail. 
All that matters right now is that that you can compress a folder like this:

```
tar -czv -f ARCHIVE_NAME.tar.bz /folder/to/compress
```
This will **c**reate an archive that is g**z**ip compressed and be **v**erbose. 
It will create the archive **f**ile "ARCHIVE_NAME.tar.bz" and will put into it the path defined in the final argument.

gzip compression is fairly slow. 
If you have lots of files you can compress in parallel (using all cores) using parallel bzip:
```
tar -I lbzip2 -cv -f ARCHIVE_NAME.tar.bz /folder/to/compress
```

* `rsync` over `ssh`
* Compressing files using parallel algorithms: `tar` and `lbzip2`. Demo.

```bash

```
---





# Searching for files
This section will just provide examples showing how commands can be chained together to do things that are surprisingly complicated. 
The main take home point is that this sort of thing is possible, we won't go into all the details why everything here works. 
Let's SSH to joiner and go to the directory containing summaries of all the acquisitions done on BrainSaw.

```
$ /mnt/data/BakingTrayStacks/ADMIN/acquisitionStats
```

e.g.
```
$ ls -l akrami/anatomy/virus_tests/VP_CAP01
total 220
-rwxr-xr-x 1 kiosk users 220394 Mar  1 16:49 acqLog_VP_CAP01.txt
-rwxr-xr-x 1 kiosk users   2311 Mar  1 16:49 recipe_VP_CAP01_210921_110016.yml
```

If we can find all the "recipe" files and count them we will know how many samples were acquired.
```
$ find . -name '*recipe*'
```

Woah! That's a lot of stuff!
We can "pipe" the standard output of `find` to `wc`, the word count, command using the `|` operator:

```
$ find . -name '*recipe*' | wc -l
4372
```

So there are over four thousand recipe files. 

This is how we list only the file names and sort them alphabetically:
```
 find . -name '*recipe*' -printf '%f\n' | sort | less
```

How many of those file names are unique?
```
$ find . -name '*recipe*' -printf '%f\n' | sort | wc -l
4372

$ find . -name '*recipe*' -printf '%f\n' | sort | uniq | wc -l
3948
```
For whatever reason about 400 recipe names are copies. 

You can use the `-exec` flag to `find` to run an operation on each file. 
For example, count the number of lines in each file:

```
$ find . -name '*recipe*' -exec wc -l {} \;
```

We can go crazy and find the number of lines in these files and how often this occurs:
```
$ find . -name '*recipe*'  -type f -exec wc -l {} \;  | sed 's/ .*//' | sort | uniq -c
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





### These operations can work on remote content too!
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
* Further reading on the above at the [Software Carpentry Course](https://swcarpentry.github.io/shell-novice/01-intro/index.html)
* Try some fancier modern stuff: switch from `bash` to `zsh` and try [PowerLevel10k](https://github.com/romkatv/powerlevel10k) and [fzf](https://github.com/junegunn/fzf).
