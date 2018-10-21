# Commands for docker

## Uninstall old versions

Older versions of Docker were called `docker` or `docker-engine`. If these are installed, uninstall them:

```$ apt remove docker docker-engine docker.io```

## Install using the repository

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

### SET UP THE REPOSITORY

1. Update the `apt` package index:

```apt update```

2. Install packages to allow `apt` to use a repository over HTTPS:

``` bash

apt -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common

```

3. Add Docker’s official GPG key:

```$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -```

Verify that you now have the key with the fingerprint `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`, by searching for the last 8 characters of the fingerprint.

```bash

$ apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22

```

4. Use the following command to set up the *stable* repository. You always need the *stable* repository, even if you want to install builds from the edge or test repositories as well. To add the edge or test repository, add the word `edge` or `test` (or both) after the word `stable` in the commands below.

To also add the *edge* repository, add `edge` after `stable` on the last line of the command.

```bash

add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

```

Note: Starting with Docker 17.06, stable releases are also pushed to the edge and test repositories.

### INSTALL DOCKER CE

1. Update the apt package index.

```bash

apt -y update

```

2. Install the latest version of Docker CE, or go to the next step to install a specific version:

```bash

apt -y install docker-ce

```

3. To install a specific version of Docker CE, list the available versions in the repo, then select and install:
   a. List the versions available in your repo:

```bash

$ apt-cache madison docker-ce
docker-ce | 18.03.0~ce-0~debian | https://download.docker.com/linux/debian jessie/stable amd64 Packages

```

   b. Install a specific version by its fully qualified package name, which is the package name (docker-ce) plus the version string (2nd column) up to the first hyphen, separated by an equals sign (=), for example, docker-ce=18.03.0.ce.

```bash

apt -y install docker-ce=<VERSION_STRING>

```

The Docker daemon starts automatically.

### Verify that Docker CE is installed correctly by running the hello-world image

```bash

sudo docker run hello-world

```

This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

Docker CE is installed and running. The docker group is created but no users are added to it. You need to use sudo to run Docker commands.

## Manage Docker as a non-root user

The Docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user `root` and other users can only access it using `sudo`. The Docker daemon always runs as the `root` user.

If you don’t want to preface the `docker` command with `sudo`, create a Unix group called docker and add users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group.

To create the `docker` group and add your user:

1. Create the `docker` group.

```sudo groupadd docker```

2. Add your user to the `docker` group.

```sudo usermod -aG docker $USER```

3. Log out and log back in so that your group membership is re-evaluated.

If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

On a desktop Linux environment such as X Windows, log out of your session completely and then log back in.

4. Verify that you can run `docker` commands without `sudo`.

```$ docker run hello-world```

This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

If you initially ran Docker CLI commands using `sudo` before adding your user to the `docker` group, you may see the following error, which indicates that your `~/.docker/` directory was created with incorrect permissions due to the `sudo` commands.

```bash

WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied

```

To fix this problem, either remove the `~/.docker/` directory (it is recreated automatically, but any custom settings are lost), or change its ownership and permissions using the following commands:

```bash

sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R

```

## Configure Docker to start on boot

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use `systemd` to manage which services start when the system boots. Ubuntu 14.10 and below use `upstart`.

### systemd

```bash

sudo systemctl enable docker

```

To disable this behavior, use `disable` instead.

```bash

sudo systemctl disable docker

```

### upstart

Docker is automatically configured to start on boot using `upstart`. To disable this behavior, use the following command:

```$ echo manual | sudo tee /etc/init/docker.override```

### chkconfig

```$ sudo chkconfig docker on```

## Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

### Prerequisites

Docker Compose relies on Docker Engine for any meaningful work, so make sure you have Docker Engine installed either locally or remote, depending on your setup.

- first install the Docker for your OS as described on the Get Docker page, then come back here for instructions on installing Compose on Linux systems.
- To run Compose as a non-root user

### Install Compose on Linux systems

On Linux, you can download the Docker Compose binary from the Compose repository release page on GitHub. Follow the instructions from the link, which involve running the `curl` command in your terminal to download the binaries. These step by step instructions are also included below.

1. Run this command to download the latest version of Docker Compose:

```bash

sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```

#### Use the latest Compose release number in the download command

`The above command is an example, and it may become out-of-date. To ensure you have the latest version, check the Compose repository release page on GitHub.`

2. Apply executable permissions to the binary:

```bash

sudo chmod +x /usr/local/bin/docker-compose

```

3. Test the installation.

```bash

$ docker-compose --version
docker-compose version 1.22.0, build 1719ceb

```

### Uninstallation

To uninstall Docker Compose if you installed using curl:

```bash

sudo rm /usr/local/bin/docker-compose

```

## Install command completion

### Bash

Make sure bash completion is installed.

- On a current Linux OS (in a non-minimal installation), bash completion should be available.

