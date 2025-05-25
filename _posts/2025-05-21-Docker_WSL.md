---
title: Docker - Windows/WSL
data: 2025-05-21 21:18:00 -0600
categories: [docker]
tags: [linux,docker]
description: Docker Desktop Personal, time to play with Docker.
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>If you don't have any other hardware to use in your home lab at the moment we can play with Docker in the Docker Desktop for Windows playground. I would not use this solution for anything you want to keep around for any given time, but it will let you get started.
{: .prompt-info }

Docker is a container engine that is extremely popular for testing application, app isolation, and ease of setup. Many of the services that you may want to run in your home lab have docker container install options. Let's dive in and get the Windows Docker Desktop Personal Edition up and running.

## Docker Desktop Installation
- You will need to create a docker account in order to download the docker desktop app. Head over to [Docker's Website](https://docs.docker.com/desktop/setup/install/windows-install/) and start the download and registration for Docker Desktop for Windows.
- Select the download for Docker **Desktop for Windows - x86_64**.
- During the Setup phase make sure you select Docker for WSL as the backend engine.
- You will be taken to the docker desktop homepage to setup a docker account. Use the same email you have been using for your home lab.
- Once setup is complete you will be asked to reboot.
- Log back into Windows and Docker Desktop should auto-launch.
- The recent install process is much better at setting user permissions for docker to run as our WSL user, but we will want to verify just in case.
- Right-Click on the Window Start Launcher and Select **Computer Management**.
- From the left menu select **Local Users and Groups** then the Groups Folder.
- Right-Click on the **docker-users** group and select Properties.
- Verify that your local user account is listed in the members list. If it is not add it.
- Close Computer Manager.
- Open your Windows Terminal to access your WSL install.
- Run the following command and make sure that your WSL user ID is listed:

```bash
sudo cat /etc/group | grep docker
```
## Verify your Docker instance is running
- Open a Windows Terminal to access your WSL install.
- Run the following command to make sure we can build and run docker commands:

```bash
docker run hello-world
```

- If it was successful, you will see a message about downloading the image then you should see the **Hello from Docker!** message indicating your installation is working.
- If you run into any errors, check out the Docker [Troubleshooting](https://docs.docker.com/desktop/troubleshoot-and-support/troubleshoot/) Site for some steps to take to troubleshoot your install.

>Congratulations! You are now ready to run docker commands locally on your WSL install in Windows.
{: .prompt-info }

>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.