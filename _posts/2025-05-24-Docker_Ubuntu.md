---
title: Docker - Ubuntu Install
data: 2025-05-24 20:57:00 -0600
categories: [docker,ubuntu]
tags: [docker]
description: Install the Official Docker Engine on Ubuntu
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>Want to add Docker to a new Ubuntu server? Let's go through the process of installing it on a new server!
{: .prompt-info }

The Official Docker Engine is the recommended method from Docker to install docker on your Ubuntu server. The Ubuntu maintainers version can has some weird affects on containers on occasion.

## Cleanup Any Old Installs
- It is recommended that you make sure there are no older versions of docker installed by the Ubuntu maintainers, so let's remove any dependencies first.
- Remote into your Ubuntu server using your username and password or [SSH Key](https://hydrahacksdocs.github.io/posts/Ssh/).
- Execute the following commands to remove any old docker application versions on the server:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc;
do sudo apt remove $pkg;
done
```

- Now remove any images, containers, and volumes left over. You may get errors if these don't exist, it is ok to ignore them:

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

- Now remove any old source lists from apt and certificate keys from the keyring:

```bash
sudo rm /etc/apt/sources.list.d/docker.list
sudo rm /etc/apt/keyrings/docker.asc
```

## Add Docker Official Repos to Ubuntu
- Use the following commands to add the key chain file to Ubuntu:

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

- Use the following commands to add the official Docker repository to Ubuntu:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```

- Now install the official docker packages to Ubuntu:

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- Make your user able to run docker commands without being root. (This does expose your docker environment a bit, so use you own judgement if you want to do this or not):

```bash
sudo usermod -aG docker $USER
```

- You will need to log out and back into your Ubuntu server for this change to take affect.
- Check the status of the docker service:

```bash
sudo systemctl status docker
```

- Enable and start the new Docker Engine if it did not get started during install

```bash
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

- Now let's make sure you can successfully run a docker deploy:

```bash
docker run hello-world
```

## What's Next?
- Check out the [Docker Documentation](https://docs.docker.com/get-started/) to learn more about Docker.
- Check out some of my [Docker Hacks](https://hydrahacksdocs.github.io/tags/docker/) for more projects you can use in your own home lab.


>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.