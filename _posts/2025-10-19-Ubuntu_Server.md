---
title: Ubuntu Server Installation & Initial Configuration
data: 2025-10-19 16:56:00 -0600
categories: [proxmox,virtualization,ubuntu]
tags: [proxmox,ubuntu]
description: Ubuntu Server Installation & Initial Configuration
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>Wether you are installing Ubuntu Server into a new VM, or installing on bare metal, this guide will help you get Ubuntu Server up and running to that you can start hosting your own services.
{: .prompt-info }

In my previous Hack I showed you how to create a [Virtual Machine](https://hydrahacksdocs.github.io/posts/Virtual_Machine/) on [Proxmox](https://hydrahacksdocs.github.io/posts/Proxmox/) in preparation to install Ubuntu Server. This Hack to work for both VM or bare metal installs however. If you want to install it as a VM, you can refer to my previous Hacks to get you ready to go.

## Pre-Requisites
You will need to consider if you will be installing Ubuntu Server on a VM or bare metal. Each will have their own needs. You can follow my Hacks for Proxmox and Create a VM to help you setup your VM Configuration File. If you want to install on bare metal I have a Hack to help you create a bootable USB drive with [YUMI](https://hydrahacksdocs.github.io/posts/Yumi/), a multi-boot USB drive creation tool.
You will also want to understand your networking requirements as well as what you plan to use the Ubuntu Server install for, so you can make sure you configure enough CPU, Memory and Drive Space for the intended purpose. Once you understand these needs, let get started.

## Install Ubuntu Server Edition
- Boot your VM or server with the ISO image you downloaded from Canonical. You will see the following boot menu. Select *Try or Install Ubuntu Server to get started.

    ![Boot Menu](/assets/posts/2025-10-19/10-ubuntu-boot.png) {: width="300" }
    _Boot Menu_

- Select your language from the list and hit **Enter** to continue the installation.

    ![Language](/assets/posts/2025-10-19/11-ubuntu-language.png) {: width="300" }
    _Language_

- If you happen to be running an older version of the installer, you can opt to update the installer or continue without updating. Make your selection then press **Enter** to continue.

    ![Update Installer](/assets/posts/2025-10-19/12-ubuntu-installer.png) {: width="300" }
    _Update Installer_

- The installer should auto-detect your keyboard layout, but if it does not, select the correct layout and variant from the drop down menu options then press **Enter** when ready to continue.

    ![Keyboard](/assets/posts/2025-10-19/13-ubuntu-keyboard.png) {: width="300" }
    _Keyboard_

- Next you can choose to install the full Ubuntu Server experience or just just the minimized version used for containers and IoT devices. In most cases you will select the Ubuntu Server option. Press **Enter** when ready to move on.

    ![Version Type](/assets/posts/2025-10-19/14-ubuntu-type.png) {: width="300" }
    _Version Type_

- The installer should detect your network hardware and give you the option to setup how you want to use it. The default is to use DHCPv4 and it will try to pull and IP address automatically for you. If you have more than one network card installed or virtual network card setup, make sure you select the correct card for each network you intend to configure. If you choose, you can also create the network configuration manually. Once you have completed your setup, continue to the next step by pressing **Enter**.

    ![Networking](/assets/posts/2025-10-19/15-ubuntu-network.png) {: width="300" }
    _Networking_

- Enter any Proxy servers that you may have on your network, or leave it blank if none are installed. Press **Enter** to continue.

    ![Proxy Server](/assets/posts/2025-10-19/16-ubuntu-proxy.png) {: width="300" }
    _Proxy Server_

- Next the installer will want to verify that you have internet connectivity so it can pull updates as needed during the install. Once it is complete you can press **Enter** to continue. If you get an error from the installer, go back and make sure your networking settings are correct.

    ![Mirror Testing](/assets/posts/2025-10-19/17-ubuntu-mirrors.png) {: width="300" }
    _Mirror Testing_

- Now you will get an option to configure your drives. You can select the drive you want to use as the OS install drive as well as if you want to use the entire disk as well as configure it as a LVM disk. LVM allows for greater flexibility and is the recommended. Choose if you want to encrypt the drive as well. Once you are satisfied with your choices, press **Enter** to continue to partitioning.

    ![Disks](/assets/posts/2025-10-19/18-ubuntu-disks.png) {: width="300" }
    _Disks_

- The installer will recommend a storage layout for you. You can opt to use the default and continue. I would review this closely however as the installer may not choose to use the entire volume group size for the root logical volume. If you do not plan to add any other logical volumes during installation, you may want to adjust it to use the full disk space. Press **Enter** once you are happy with the layout.

    ![Storage Layout](/assets/posts/2025-10-19/19-ubuntu-partitions.png) {: width="300" }
    _Storage Layout_

- Next the installer will warn you that this process is destructive to any existing data and request you wish to continue  the installation. Press **Enter** when ready.

    ![Format Disks](/assets/posts/2025-10-19/20-ubuntu-format.png) {: width="300" }
    _Format Disks_

- Now you will be prompted to create your primary user account. This account is going to be your standard login account. Enter your Name, Server Name, user ID and Password. Remember to save this to [Bitwarden](https://hydrahacksdocs.github.io/posts/Bitwarden/) if you followed my previous Hack. Press **Enter** when you are satisfied with your choices.

    ![Server Name and User Name](/assets/posts/2025-10-19/21-ubuntu-user.png) {: width="300" }
    _Server Name and User Name_

- If you have a need to upgrade your Ubuntu Server to meet more stringent security requirements you can now choose to update to Ubuntu Pro, which will help meet some of the FedRAMP, FIPS, HIPAA and other compliance hardening requirements. Press **Enter** once you have made your selection.

    ![Ubuntu Pro](/assets/posts/2025-10-19/22-ubuntu-pro.png) {: width="300" }
    _Ubuntu Pro_

- The installer will next ask you if you want to enable the OpenSSH server. I would recommend enabling the OpenSSH server if you plan to access your server remotely. It also allows you to import any [SSH Keys](https://hydrahacksdocs.github.io/posts/Ssh/) you may have previously created. Once done, press **Enter**.


    ![SSH Server](/assets/posts/2025-10-19/23-ubuntu-ssh.png) {: width="300" }
    _SSH Server_

- During installation the installer will also give you the option to install some common services. If you plan to use this installation as a docker host, I would suggest you not select the docker option here though and use the docker repositories instead. I have a different Hack that can help you install [Docker on Ubuntu](https://hydrahacksdocs.github.io/posts/Docker_Ubuntu/) if you need it. Press **Enter** when you are happy with your selections.

    ![Services](/assets/posts/2025-10-19/24-ubuntu-servers.png) {: width="300" }
    _Services_

- The installer will now begin your installation. Wait until it has completed then select Reboot Now and then press **Enter** to reboot. Your installation is now complete. Verify you can log into your new Ubuntu Server. I have few basic configuration changes to recommend after a new install, so let's explore those in the next section.

## After Install Configuration Updates
- First, let's get your new system updated with the latest security patches and kernel. First you will update the repository cache, then apply any outstanding application and kernel patches.

```bash
sudo apt update
sudo apt dist-upgrade -y
```

- Next I would copy any [SSH Keys](https://hydrahacksdocs.github.io/posts/Ssh/) you may have previously created. You can follow my Hack on SSH Keys to get help if you have not created any keys yet. This will allow you to connect to your server remotely without needing your password. This can be helpful if you plan to run any automation against your new server.

- As part of your SSH Key update, you may want to enable your user ID to run sudo commands without the need to provide your password, which is the default behavior on a Ubuntu Server installation. This will allow any automation you run against your server to perform root activities for you. As a note here, this is a dangerous config change and I would recommend that you are using a different user ID and password for your automation versus your daily driver account. Run the following command to open the sudo editor, then add the following line replacing username with your user ID. There will already be a line in the config file with similar syntax, just add the new line below the existing line. Save the file and you will be all set.

```bash
sudo visudo
```

```yaml
%sudo   username=(ALL:ALL) NOPASSWD:ALL
```

- Finally you can browse my other [Hacks](https://hydrahacksdocs.github.io/) to add more services to your new Ubuntu Server installation.


>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.