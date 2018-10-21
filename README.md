# Commands and guides

## Docker

install and setup for [docker](docker.md) on linux

## Plsql

list of basic [plsql](plsql.md) commands

## Visual Studio Code Extensions

1. Docker
2. Gitlens
3. JavaScript (ES6) code snippets
4. mardownlint
5. Material Icon Theme
6. npm

## bash Setups

### Granting Administrative Privileges

To avoid having to log out of our normal user and log back in as the *root* account, we can set up what is known as "superuser" or *root* privileges for our normal account. This will allow our normal user to run commands with administrative privileges by putting the word `sudo` before each command.

To add these privileges to our new user, we need to add the new user to the *sudo* group. By default, on Debian 9, users who belong to the *sudo* group are allowed to use the `sudo` command.

As *root*, run this command to add your new user to the *sudo* group (substitute with your user):

```bash

usermod -aG sudo carlitoks

```

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
