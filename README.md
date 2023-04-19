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
If you do not already have [homebrew](https://brew.sh/) installed, first do:

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


## User demos
