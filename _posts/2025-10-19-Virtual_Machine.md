---
title: Proxmox Virtual Machine Deployment
data: 2025-10-19 16:06:00 -0600
categories: [proxmox,virtualization]
tags: [proxmox]
description: Proxmox Virtual Machine Deployment
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>Now that you have Proxmox installed, let's create our first VM.
{: .prompt-info }

With Proxmox now installed, let prepare your new installation to build our first VM. We are going to download an ISO image for Ubuntu Server and then configure the VM for deployment to Proxmox. After we are done, I will walk you through the installation of [Ubuntu Server Installation](https://hydrahacksdocs.github.io/posts/Ubuntu_Server/) in a different Hack.

## Download the ISO Needed for Ubuntu Server
- Log into your Proxmox server and select your server from the left menu.
- If you have not yet added external storage to your Proxmox server select the **local** storage.
- Select the **ISO Images** from the right hand context menu.

    ![Local Storage ISO Images](/2025-10-19/000-ubuntu-local-iso.png) {: width="300" }
    _ISO Images_

- At the top of the page select **Download from URL** option. You can try to upload the ISO if you have downloaded it to your computer already, but I find it is usually faster to just download it with Proxmox.
- Copy a URL from the [Ubuntu Alternate Downloads](https://launchpad.net/ubuntu/+cdmirrors) page matching your region.
- Paste the URL into the URL field and click on **Query URL**. This will validate the URL you entered and fill in the ISO image name for you. Now click on **Download and wait for it to complete.

    ![URL Download](/2025-10-19/000-ubuntu-iso-download.png){: width="300" }
    _URL Download_

## Create the New VM Configuration File
- At the very top of the Proxmox server page you will see a button to **Create VM**. Click on this button to start the VM creation wizard.

    ![Create VM](/2025-10-19/00-ubuntu-create-vm.png) {: width="300" }
    _Create VM_

- Fill in the Node (Proxmox Server Name), VM ID (Must be a unique number), and Name for the VM. You can also check the box to Start at boot to ensure the VM starts every time your Proxmox server reboots. You can also set any Startup/Shutdown order or delay you may need. This is helpful if the VM depends on another VM being up and running. An example of this my be if you have a PostgreSQL database VM that needs to be up and running before your website front end server is started. Once done, click on **Next**.

    ![VM Name](/2025-10-19/01-ubuntu-name.png) {: width="300" }
    _VM Name_

- Next you need to choose the ISO location and ISO image you want to use as well as the Guest OS. For our Ubuntu install select Ubuntu Server ISO you downloaded earlier as well as Linux type and 6.x - 2.6 Kernel Version. Click on **Next** when ready to move to the next step.

    ![VM OS](/2025-10-19/02-ubuntu-iso.png) {: width="300" }
    _VM OS_

- Now you need to choose what type of hardware BIOS you want to use as well as the type of drive controller you want to use. You can use the default if you choose, I have selected a VM type that will support a UEFI BIOS as well as a TPM Security Chip. You will need to select the storage location for the BIOS and TPM on this page. If you don't want to use the UEFI/TPM options, just leave them unchecked. Once ready, click on **Next** to proceed.

    ![BIOS Config](/2025-10-19/03-ubuntu-hardware.png) {: width="300" }
    _BIOS Config_

- Choose your hard drive options next. Select the Storage location (You will only have local storage if you have not setup remote SAN/NAS storage yet.), Disk Size, and any relevant options. then click on **Next** when ready.

    ![Disks](/2025-10-19/04-ubuntu-disks.png) {: width="300" }
    _Disks_

- Next setup the CPU Socket (Most likely 1 unless you have multiple physical CPUs in the host.), number of Cores and any advanced options you may need. Click on **Next** once complete.

    ![CPU](/2025-10-19/05-ubuntu-cpu.png) {: width="300" }
    _CPU_

- Enter the amount of RAM that you want to assign to the VM in MiB. Example here is 4GB of RAM. Select **Next** when ready to move on.

    ![Memory](/2025-10-19/06-ubuntu-memory.png) {: width="300" }
    _Memory_

- Next you can configure your networking settings. In most cases you will use the default Bridge with no VLAN tagging. If you need these options you should have already configured your network to support VLAN tagging. Once ready click on **Next** to proceed.

    ![Networking](/2025-10-19/07-ubuntu-network.png) {: width="300" }
    _Networking_

- On the Confirm page, review your settings. Once you are satisfied click on finish to create the VM configuration. If you are ready to install the OS and don't need to configure any advanced options, you can select the **Start after created** checkbox and the installation of the OS will begin as soon as the VM configuration is complete. Click on **Finish** when ready to create the VM configuration.

    ![Confirm](/2025-10-19/08-ubuntu-finish.png) {: width="300" }
    _Confirm_

Congratulations! You have created your first VM configuration and are ready to install your first Virtual OS. If you would like to continue with the installation of Ubuntu, follow me to the next Hack [Ubuntu Server Installation](https://hydrahacksdocs.github.io/posts/Ubuntu_Server/).

>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.