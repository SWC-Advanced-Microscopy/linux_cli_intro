# Linux Command Line Intro

This is a presentation on the Linux command line for beginners. 
It is written is markdown and run at the command line with [slides](https://github.com/maaslalani/slides).

## Installation
To run the presentation itself you will need to install [slides](https://github.com/maaslalani/slides) plus some additional programs

<details>
<summary>Linux</summary>

```bash
sudo apt install figlet cmatrix cowsay jp2a snap
sudo snap install slides
```
**NOTE:** On at least Ubuntu, the snap install does not handle code execution properly. 
You could try installing via `go` (see the project README) or download the binary from the releases page and add to your path. 
</details>

<details>
<summary>Mac with homebrew</summary>
If you do not already have homebrew installed, first do:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then:
```bash
brew install slides figlet cmatrix cowsay jp2a 
```
</details>


## Running the presentation 
The presentation must be executable. 
There are short scripts that do this then run it:

```bash
cd md_presentation
./run_linux_cli.md 
```

or

```bash
cd md_presentation
./run_linux_history.md 
```

## Software for attendees to install
Those attending the course will need to install the following

### On Mac
People will [HomeBrew](https://brew.sh/) and then can:
```
brew install rsync lbzip2 htop nload nano vim ncdu curl wget telnet cowsay
```

### On Windows
People will need to install Ubuntu on the [Windows Subsystem for Linux](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview). 
Then they can follow the `apt` command, below:


### Linux
On Ubuntu/Debian people can:

```
apt install rsync lbzip2 htop nload nano vim ncdu curl wget telnet cowsay
```

If none of the above works, you could set up a Linux server with a temporary account and have people SSH into that. 
We therefore will do SSH first in the presentation, including how to do it with a shared key. 

Attendees can edit the markdown files [Typora](https://typora.io/) or any text editor.

## Also to do in advance
All attendees should make sure they can ssh to bastion. 


## Alternatives to command line slides
There are, of course, better alternatives to doing you presentation at the command line. These include:
* [remark](https://github.com/gnab/remark) is a nice markdown-based system that is pretty simple [and looks good](https://remarkjs.com/#1). 
* [slidev](https://sli.dev/) is also markdown-based but a little more complicated. 
* [reveal.js](https://github.com/hakimel/reveal.js/) is an HTML/CSS-based system that perhaps [looks better](https://revealjs.com/demo/) than the above but is a little more complicated. 

All the above are really good for presenting code, as they incorporate syntax highlighting and, at least in the case of reveal, allows highlighting and fading of specific lines of code as you move through slides.


## Easy Access Links
* [https://tinyurl.com/linuxCLIintro](https://tinyurl.com/linuxCLIintro) points to the GitHub repo page.

* You can clone the repo with `git clone https://tinyurl.com/linuxCLIintroGit`
