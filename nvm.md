# Install node js Using NVM

An alternative to installing **Node.js** through `apt` is to use a tool called **nvm**, which stands for *"Node.js Version Manager"*. Rather than working at the operating system level, **nvm** works at the level of an independent directory within your home directory. This means that you can install multiple self-contained versions of **Node.js** without affecting the entire system.

Controlling your environment with **nvm** allows you to access the newest versions of **Node.js** and retain and manage previous releases. It is a different utility from `apt`, however, and the versions of **Node.js** that you manage with it are distinct from those you manage with `apt`.

To download the nvm installation script from the [project's GitHub page](https://github.com/creationix/nvm), you can use `curl`. Note that the version number may differ from what is highlighted here:

```bash
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh -o install_nvm.sh
```

Inspect the installation script with vim

```bash
vim install_nvm.sh
```

Run the script with bash:

```bash
bash install_nvm.sh
```

It will install the software into a subdirectory of your home directory at `~/.nvm`. It will also add the necessary lines to your `~/.profile` file to use the file.

To gain access to the **nvm** functionality, you'll need to either log out and log back in again or source the `~/.profile` file so that your current session knows about the changes:

```bash
source ~/.profile
```

With **nvm** installed, you can install isolated **Node.js** versions. For information about the versions of **Node.js** that are available, type:

```bash
nvm ls-remote
```

As you can see, the current LTS version at the time of this writing is v8.11.1. You can install that by typing:

```bash
nvm install 8.11.1
```

Usually, **nvm** will switch to use the most recently installed version. You can tell nvm to use the version you just downloaded by typing:

```bash
nvm use 8.11.1
```

When you install **Node.js** using **nvm**, the executable is called `node`. You can see the version currently being used by the shell by typing:

```bash
$ node -v
v8.11.1
```

If you have multiple **Node.js** versions, you can see what is installed by typing:

```bash
nvm ls
```

If you wish to default one of the versions, type:

```bash
nvm alias default 8.11.1
```

This version will be automatically selected when a new session spawns. You can also reference it by the alias like this:

```bash
nvm use default
```

Each version of **Node.js** will keep track of its own packages and has npm available to manage these.

[Source](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-debian-9)