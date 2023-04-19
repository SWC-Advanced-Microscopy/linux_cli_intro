# Linux Command Line Intro


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
If necessary run:
```bash
chmod +x md_presentation/linux_cli.md 
```

Then 
```bash
cd md_presentation
slides linux_cli.md 
```



## Demos
To initially show people surprising things the CLI can do, you can try the following. 

* Have `cmatrix` running in the background whilst people take their seats. 
* Demo `curl wttr.in/London` you can `alias weather='curl wttr.in/London'`
* Demo `telnet mapscii.me` you can `alias maps='telnet mapscii.me'`
* Point out these things are not necessarily useful, but they are cool and in that spirit the presentation will be done on the CLI

## Software attendees will need

On Mac:
```
brew install rsync lbzip2 htop nload nano vim ncdu curl wget telnet cowsay
```

or Linux/WSL:

```
apt install rsync lbzip2 htop nload nano vim ncdu curl wget telnet cowsay
```

For people who fail to achieve either of the above you could set up a Linux server with a temporary account and have people SSH into that. 
We therefore will do SSH first in the presentation, including how to do it with a shared key. 


## Alternatives
There are, of course, better alternatives to doing you presentation at the command line. These include:
* [remark](https://github.com/gnab/remark) is a nice markdown-based system that is pretty simple [and looks good](https://remarkjs.com/#1). 
* [slidev](https://sli.dev/) is also markdown-based but a little more complicated. 
* [reveal.js](https://github.com/hakimel/reveal.js/) is an HTML/CSS-based system that perhaps [looks better](https://revealjs.com/demo/) than the above but is a little more complicated. 

All the above are really good for presenting code, as they incorporate syntax highlighting and, at least in the case of reveal, allows highlighting and fading of specific lines of code as you move through slides.

