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
figlet -k -w 150 -c  "The   Linux   Command   Line" 
~~~
```
```
~~~bash
figlet -k -w 150 -c "a   practical   guide"
~~~
```


---
## Make sure you have installed everything

### On Mac
```
brew install rsync lbzip2 htop nload nano vim ncdu curl wget telnet
```

### On Linux
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

## What Is Linux?
* Where it came from?
* When?
* What is a "distribution"?
* What is a desktop environment?
* What is the command line?
---



## Image
```
~~~bash
jp2a --colors ./assets/tux.jpg
~~~
```

---



## SSH
* Logging onto machines with SSH. 
* Reaching your Linux PC from home without VPN.
* Setting up passwordless SSH using a shared key (Copy your SSH key (ssh-copy-id) There are multiple ways to achieve this however this command is a shortcut that saves time. What does it actually do? This command replicates what you can also do manually. Copying the ~/.ssh/id_rsa.pub (or the default) key from your system and adds it to an ~/.ssh/authorized_keys file on the remote server.

```
localhost:~$ ssh-copy-id user@remoteserver
```
---

## Mount Points

People get confused about this one a good deal.
---

# Basic CLI commands

* Basic details:
    * Directory structure and navigating it: `ls`, `pwd`, `cd` and tab for auto-complete
    * Highlight then middle click to copy/paste
    * The above are commands and you can get help: `man`, `–help`
* Creating files
    * `touch`
    * nano/vim/emacs (just what they are in less than 5 minutes). How to quit from `vi` and `emacs`!
    * redirect output (`>`, `>>`)
    * Pipes
* Displaying/printing file contents
    * echo, cat, less, head, tail (or cat ~/.ssh/config | cowsay)
* Moving/renaming/deleting files
    * `mv`, `rm`, `cp`, `mkdir`
* Wildcards
* ctrl-c
* `watch`
* Cautions
* Deleting files is forever
* Spaces in filenames
* Funny characters
* `uniq` and `sort`
* Mention Bash scripts as a thing but no further details. 


---

## Code execution
```python
print("HELLO %s" % "world")
```

You can execute code inside your slides by pressing `<C-e>`,
the output of your command will be displayed at the end of the current slide.

---
