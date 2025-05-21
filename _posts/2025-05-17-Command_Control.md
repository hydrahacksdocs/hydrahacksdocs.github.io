---
title: Home Lab - Command & Control
data: 2025-05-17 23:17:00 -0600
categories: [homelab]
tags: [getting_started,homelab]
description: How to setup a command & control machine for your home lab.
author: hydra
media_subpath: /assets/posts/
pin: true
---
# Synopsis
>So you want to build a home lab? Let's get your command & control machine ready for the task!
{: .prompt-info }

What is a command & control machine? Basically, you need a machine that has all the tools that you need to build, configure, manage, and deploy your home lab. This Hack is meant to give you a starting place. This Hack assumes you are using a Windows 11 computer, but many of the concepts can be applied to a Linux or Mac machine as well. I will also make this as simple, follow along as possible, but some experience with a Windows computer is at least required.

## Suggestions and Recommendations
None of these are requirements, but I find that a clean, lab focused environment is helpful to put me in the correct mindset.

- Create a new [User Account](https://support.microsoft.com/en-us/windows/manage-user-accounts-in-windows-104dc19f-6430-4b49-6a2b-e4dbd1dcdf32) on your Windows computer:
  - This is helpful to give you a clean space free from your daily distractions and help you focus on your goals for your home lab.
- Create a new email address for your home lab account:
  - Creating a dedicated email account allows you to send logs and register for accounts online dedicated to your home lab. This helps to keep your daily email traffic segregated. You can use your favorite free email provider like [Gmail](https://mail.google.com) or [Outlook](https://www.microsoft.com/en-gb/microsoft-365-life-hacks/organisation/how-to-create-outlook-email-account).
- Security:
  - Many of the services that you can setup in your home lab can put the rest of your home network at risk. Follow best practices and set difficult passwords, manage firewall rules, and understand the risks before deploying anything.
- Don't rush out and buy a bunch of hardware:
  - Your home lab can grow over time, don't think you need to spend a ton of money to have a functional home lab. Be realistic about your needs and goals. We will discuss hardware in future Hacks.
- Have Fun:
  - The point of a home lab is to learn. Enjoy the process of building something yourself. Screw stuff up so you can learn from it. Don't expect perfection. Ask yourself what your goal is for installing any given service so you don't overload yourself. Start out slow, you don't need enterprise level gear or expertise to have a fun, functional home lab. You don't need every service someone else installs, be picky about what you are willing to support into the future.

## Command & Control Software Recommendations
Let's take a moment to look at some of the software you may want to use to help setup your command & control computer. Each package will have its own install Hack that you can follow, just click the links to be taken to each Hack. You don't have to do these in order, but I try to list them in an order that worked for me.

- Google [Chrome Browser](https://www.google.com/chrome)
  - Personal preference, you can use any modern browser as long as it supports some of the addons you may need.
- [Bitwarden Personal Account](https://bitwarden.com/products/personal/)
  - Password/SSH Key Management/Authenticator
  - I highly recommend you get the premium account ($10/year) as it adds some useful features, like password monitoring on the dark web and a built in Authenticator for TOTP.
  - Here is my [Bitwarden Hack](https://hydrahacksdocs.github.io/posts/Bitwarden/) for some tips and getting started with Bitwarden.
- [Windows Subsystem for Linux](https://hydrahacksdocs.github.io/posts/WSL/) (WSL) with Ubuntu Linux
  - Yes, most of your home lab services will be running on Linux in some form. Don't stress, I'll try to make it as simple as possible for you to follow along.
- [Microsoft Visual Studio Code](https://hydrahacksdocs.github.io/posts/VS_Code/)
  - VS Code is a good, lightweight, cross-platform editor with lots of community support and extra addons. Don't confuse it with Visual Studio MSDN though as it is intended for the serious developer running various application code on your local machine. You will not need a Microsoft Visual Studio MSDN account to use VS Code.
- GitHub Account (Optional, but recommended)
  - It is highly recommended that you keep your home lab documented. GitHub is a online git repository that offers free accounts to developers, and in most cases, you will not need anything more than a free account for home lab.
  - I have a [Hack](https://hydrahacksdocs.github.io/posts/GitHub/) to help you get setup with a free account and how to setup your WSL to interact with it through SSH keys.
- [SSH Hack](https://hydrahacksdocs.github.io/posts/Ssh/) (Secure Shell)
  - SSH is the method that we will use to connect to all remote Linux machines in the home lab as well as our git repository.
  - SSH is installed in WSL, but we can also install [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) if you want a Windows based tool for SSH remote control.
- [Git for Windows](https://git-scm.com/downloads)
  - Optional, you can do everything from your WSL.
- Docker Desktop for Windows or Docker on your WSL
  - Optional for your Command & Control computer, but if you don't have any other hardware to play with yet, you can use your command & control machine to play with some docker services.
- [RaspberryPi Imager](https://www.raspberrypi.com/software/)
  - The RaspberryPi is a Single Board Computer (SBC) ths is popular in home lab as a low cost entry point. It have a massive community with lots of project based on it. If you are looking for an inexpensive introduction to Linux hardware you can't go wrong. If you don't already have one, I would suggest you look at the RaspberryPi 5 at a minimum starting point.
- [BalenaEtcher](https://etcher.balena.io/)
  - Many of the projects that you will be working on in your home lab will require a way to write an OS image to a USB thumb drive. BelenaEtcher is a widely supported, simple tool used to write images. [Rufus](https://rufus.ie/en/) is another option with more customization. If you want multi-boot capabilities you may want to look at [YUMI](https://pendrivelinux.com/yumi-multiboot-usb-creator/) as an option too.

## Basic Hardware Needs
You don't need much hardware to start your home lab journey, so don't go overboard. You can expand as you decide to add more services.

- Windows Laptop or Desktop for Command & Control
  - If you want to run some services before buying more hardware try to have at least 16GB of RAM and a recent CPU.
- Wireless or hardwired network connection for Internet access
  - Everything we do will require us to download software packages, install updates, and pull docker images.
- Cellphone (Optional for Bitwarden App)

## What's Next?
Now that you have your command & control computer ready to go, you can start to look at other services that I have Hacks for. If you're just getting started I would suggest looking at some of the Docker Hacks or even the RaspberryPi Hacks as they both have a lower cost for entry.


>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.