# Commands for docker

##  Uninstall old versions
Older versions of Docker were called `docker` or `docker-engine`. If these are installed, uninstall them:
``` $ apt-get remove docker docker-engine docker.io ```
## Install using the repository
Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

### SET UP THE REPOSITORY
1. Update the `apt` package index:
``` $ apt update ```
2. Install packages to allow `apt` to use a repository over HTTPS:

``` 
$ apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
```
3. Add Docker’s official GPG key:
``` $ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - ```

Verify that you now have the key with the fingerprint `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`, by searching for the last 8 characters of the fingerprint.
```
$ apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```
Use the following command to set up the *stable* repository. You always need the *stable* repository, even if you want to install builds from the edge or test repositories as well. To add the edge or test repository, add the word `edge` or `test` (or both) after the word `stable` in the commands below.

To also add the *edge* repository, add `edge` after `stable` on the last line of the command.

```
$ add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```

Note: Starting with Docker 17.06, stable releases are also pushed to the edge and test repositories.