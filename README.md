# Commands and guides

## Docker

## Psql

## Visual Studio Code Extensions

1. Docker
2. Gitlens
3. JavaScript (ES6) code snippets
4. mardownlint
5. Material Icon Theme
6. npm

## bash Setups

### Multiple Terminals in one window

Use Terminator

```bash

apt install terminator

```

### Show Git Branch In Terminal

To display the current prompt setting, run:

```bash

$ echo $PS1
[\u@\h \W]$ # Sample output

```

Open the `~/.bashrc` file with your favorite text editor and add the following lines:

```bash

git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1="[[\033[36m\]\u\[\033[m\]@\h \[\033[32m\] \[\033[33;1m\]\W]\$(git_branch)\$ "

```

Load the `~/.bashrc` to apply changes for the current session without login/logout:

```bash

source ~/.bashrc

```

#### example for debian 9

```bash

PS1="${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$(git_branch)\$  "

```

Load the `~/.bashrc` to apply changes again
