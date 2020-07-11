---
title: "Auto-install dev tools on Linux"
date: 2018-01-28
tags: [automation, linux, shell]
header:
  image: "/images/bash_logo.png"
excerpt: "Automation, Linux, Shell scripting"
mathjax: "true"
---


One of the most frustrating parts of setting up a new machine is custom software installation. The most convenient way of getting through the process is using a custom installation script.  
The installation scripts have been tested on Linux Mint 19.

### TL;DR
Download the installation scripts for my web-dev and data-sci tools [here](https://github.com/orestispanago/Install-dev-tools).  

Restore home folder backup using Deja-Dup to apply custom app settings.

### Detailed version

##### 1. Web development tools

Programming languages can easily be installed from the command line, e.g. nodejs:

``` bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

or JDK8:

```bash
sudo apt-get install -y openjdk-8-jdk
```

Docker also provides a convenience script along with installation instructions. Note that I included ```usermod``` command to use docker without typing ```sudo``` all the time:
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
rm get-docker.sh
```
As far as the apps are concerned, during my first attempt, I followed these steps:
1. Downloaded the .deb files using ```wget```
1. Installed all the .deb files in the working directory
1. Installed their dependencies
1. Deleted the .deb files

as in the example below:

```bash
wget https://dev.mysql.com/get/Downloads/MySQLGUITools/mysql-workbench-community_8.0.20-1ubuntu18.04_amd64.deb
sudo dpkg -i *.deb
sudo apt-get install -f -y
rm mysql-workbench-community_8.0.20-1ubuntu18.04_amd64.deb
```
However, getting the download link manually is not obvious for all apps and a lot of PPAs were added, which did not look so neat.

I chose to install the rest of the apps using flatpak, since they are stable and they integrate well in the OS theme. As a plus, flatpak comes preinstalled with Linux Mint.

```bash
flatpak install flathub com.axosoft.GitKraken -y
flatpak install flathub com.getpostman.Postman -y
flatpak install flathub io.atom.Atom -y
flatpak install flathub org.gnome.DejaDup -y
```

Of course, ```snap``` can be used in similar way.  
[Here](https://www.youtube.com/watch?v=9HuExVD56Bo) is a nice video on packaging systems from *The Linux Experiment* channel.


To apply my custom settings to each app, I restore my home folder which I have backed up using Deja-Dup. This is a convenient way of preserving installed packages, logins, even full IDE installations, such as netbeans.
