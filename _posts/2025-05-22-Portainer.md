---
title: Portainer - WSL/Docker
data: 2025-05-21 15:25:00 -0600
categories: [docker]
tags: [portainer,docker]
description: Portainer, docker container management
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>Portainer is a web-based docker container that allows us to manage, create, update, and monitor our container environment. It has added recent support for Kubernetes as well. Let's get it installed and configured.
{: .prompt-info }

You will need Docker Compose to perform this setup. If you still only have your WSL Linux computer and hav not installed docker yet, you can use the [Docker WSL](https://hydrahacksdocs.github.io/posts/Docker_WSL/) Hack to prepare for this install.

## Installation
- Open your Windows Terminal WSL and then make sure you are in your home directory:

```bash
cd ~
```

- Create a directory to hold your docker compose services and the portainer docker-compose.yml file:

```bash
mkdir -p docker_services/portainer
cd ~/docker_services/portainer
```

- Create a docker-compose.yml file:

```bash
touch docker-compose.yml
```

- Edit the docker-compose.yml file using nano or VS Code and insert the following config:

```bash
nano docker-compose.yml
```

```bash
code docker-compose.yml
```

```bash
services:
  portainer:
    image: portainer/portainer-ce:lts
    container_name: portainer
    ports:
      - 9443:9443
      - 8000:8000
    restart: always
    volumes:
      - data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    
volumes:
  data:
    driver: local
```

>Services - defines the docker services we are going to install. Portainer - defines the service name. Image - what docker image do we need to download from the docker container registry. Container_Name - name the container so we can identify it easier later. Ports - define what port we need to map from outside:inside our container. Restart - define how we want docker to behave if the container crashes/exits. Volumes - define the volumes we need to mount inside our container. The /var/run/docker.sock is a special link that allows the container to talk to docker directly. Volumes -> Date - define the volume "data" as a local directory that docker should create at build time for us.
{: .prompt-info }

- Deploy the container:

```bash
docker compose up -d
```

>You will see it download a few images and the docker container. Wait until you are back at the command prompt again then you can check the status of the container.
{: .prompt-tip}

- Check the status of the container, it should show as "up". Repeat the command until it is listed as "up":

```bash
docker ps
```

## Initial Setup of Portainer
- Connect to the Portainer Web Interface by going to the [https://localhost:9443](https://localhost:9443) address.
- You will be asked to create an Admin Account and Password on first run. Make sure you create a nice and secure one using [Bitwarden](https://hydrahacksdocs.github.io/posts/Bitwarden/) and save it.
- Once you are able to see the Home Dashboard select local to see you local docker containers. You should see the Dashboard for the local docker, listing local containers, volumes, images, networks and stacks.
- Click on stacks. You should see the stack named portainer, for the docker compose stack we just deployed for portainer.
- Explore the interface and get comfortable with each section. You can visit [Portainer's Support](https://docs.portainer.io/user/home) for further reading.

>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.