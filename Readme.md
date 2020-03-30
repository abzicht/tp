# TP
TP - A bash/zsh tool for teleporting from one directory to another.

```text
tp --> tp -/> cd --! dc --x
```

## What it is
`tp` is just a wrapper for `cd`. It makes use of so called `portals` that point
to user defined directories.

## Why you need TP
Let's say your current working directory is `~/Documents/foo/bar/1/oak/blah`
and you quickly want to change your directory to `~/Documents/oof/rab/1/kao/halb`.
The worst thing you can do is to start entering dots into your command line:

```bash
$ cd ../../../../oof/rab/1/kao/halb
```

Since you are using both `blah` and `halb` very regularly, you often find
yourself remembering such long paths and entering such commands. You maybe
start wondering: isn't there a nice alternative to such mind numbing procedure?
Wonder no more! `tp` is here to save you.

With `tp`, switching from `~/Documents/foo/bar/1/oak/blah` to
`~/Documents/oof/rab/1/kao/halb` is done in a 7 char command:

```bash
$ tp halb
halb --> /home/user/Documents/oof/rab/1/kao/halb
```

And when you want to switch back, simply enter `tb blah`:

```bash
$ tp blah
blah --> /home/user/Documents/foo/bar/1/oak/blah
```

## Where you need TP
Everybody has a couple of static directories they use on a daily basis.
Such directories are the perfect use case for `tp`. Of course, seldom used
directories, e.g. `~/Documents/code/java/project/src/main/java/io`, do not
require a separate portal, if `~/Documents/code/java/project/` already has one.

## How you use TP
`tp` was developed with the ambition to create a minimalistic tool that offers
great ease of use.

### Setting up a portal
Before teleporting to a directory is possible, a portal must be created for that
directory:
```bash
# This creates a portal called "local" that points to ~/.local/share by
# appending it to ~/.tp_config
$ tp -a local ~/.local/share
```
Of course, you can also manually add portals by editing `~/.tp_config`
with your favorite text editor.

### TP in action
Let's assume this is your `~/.tp_config` file:

```text
up=../
r=/
root=/root
documents=/home/user/Documents/
local=/home/user/.local/share
code=/home/user/Documents/code/
bash=/home/user/Documents/code/bash
java=/home/user/Documents/code/java
proj=/home/user/Documents/code/java/proj/src/main/java/org/
py=/home/user/Documents/code/python
python=/home/user/Documents/code/python
go=/home/user/Documents/code/go
tp=/home/user/Documents/code/bash/teleport
volumes=/var/lib/docker/volumes
```

You are currently working on a python project and want to switch to your java
project. Instead of using `cd` with a (long) relative path or
inconvenient absolute path, you simply enter this command:

```bash
$ tp proj
proj --> /home/user/Documents/code/java/proj/src/main/java/org/
```

## Installation
Clone this repo and source the script:

```bash
$ git clone https://github.com/abzicht/tp && cd tp
$ source $PWD/tp
```

This does not install tp permanently, its functionality won't be present after the
next login. To permanently install tp, run

```bash
echo "source $PWD/tp" >> $HOME/.bashrc
```

once. This assumes that you use bash. For ZSH, run

```bash
echo "source $PWD/tp" >> $HOME/.zshrc
```

After running `tp` for the first time, the two files `~/.tp_config`
and `~/.tp_config.defaults` are created. Add your own portals to `~/.tp_config`
with `tp -a` or use the existing portals in `~/.tp_config.defaults`.
