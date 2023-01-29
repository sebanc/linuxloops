<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guide -->
# Installation from Windows

Linuxloops can install distros on drives or inside disk images.

## Installation on a usb flashdrive drive / sdcard

### Requirements
- x86_64 based computer with UEFI BIOS.
- Administrator access.
- Windows WSL2 installed.
- 14GB hdd space and a usb flashdrive drive / sdcard with at least 14 GB available space.

### Install guide

<details>
  <summary>Click here to open the LinuxLoops install guide for usb flashdrive drive / sdcard.</summary>

1. Open Ubuntu WSL2 and install `curl`, `cryptsetup`, `fdisk`, `tar` and `xz`.
If you intend to use the GUI installer, also make sure `x11-xserver-utils` and `zenity` packages are installed.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar x11-xserver-utils xz zenity`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/<your_username>/Downloads`
  
3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`
  
4. Launch Linuxloops install

- If your WSL version supports GUI applications, you can use the GUI installer by running:

`sudo bash ./linuxloops`

Follow the installer menu, choosing the distro, desktop environment, image path... (create the image in your Downloads folder: /mnt/c/Users/<your_username>/Downloads/distro.img)

- Otherwise using the command line:

Linuxloops arguments description:  
"-distro <distribution>": selects the linux distro (mandatory).  
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is usually selected by default).  
"-dst <path>": destination is the image path such as "/mnt/c/Users/<your_username>/Downloads/distro.img" (mandatory).  
"-s" <number>: size of the disk image in GB (optional, 14GB by default).  
"-z" <number>: size of the swap (optional) (optional, no swap by default).  
"-e": enable rootfs and swap encryption (optional but highly recommended).  
"-n": automatically install the latest nvidia proprietary driver (optional).  
"-S": automatically apply Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default) (optional).  

As an example `sudo bash ./linuxloops -distro ubuntu -env kde-full -dst /mnt/c/Users/username/Downloads/distro.img -s 24 -z 4 -e` will install ubuntu with the complete kde environment a disk image located at path "C:\Users\<your_username>\Downloads\distro.img" of 24GB size out of which 4GB are dedicated to swap and with an encrypted rootfs/swap.

5. Install Rufus and flash the file C:\Users\<your_username>\Downloads\distro.img to your usb flashdrive drive / sdcard.

6. Reboot your computer and choose your drive in the UEFI BIOS boot menu.

7. (Secure Boot enabled) You should see a blue screen, select "Enroll key from disk" -> EFI -> MOK.DER, confirm and reboot your computer.

</details>

## Installation in a disk image

### Requirements
- x86_64 based computer with UEFI BIOS.
- Administrator access.
- Windows WSL2 installed.
- Secure boot disabled.
- 14 GB available space on an unencrypted exfat or ntfs partition.

### Before you start (recommended setup)

Windows locks NTFS partitions when fast startup and hibernation are enabled, therefore the suggested approach to install LinuxLoops from Windows is to use the disk manager to reduce the main storage and create an exfat partition to store images.

Otherwise, you can install LinuxLoops on NTFS partitions but you have to make sure that bitlocker, fast startup and hibernation are disabled (refer to online resources).

### Install guide

<details>
  <summary>Click here to open the LinuxLoops install guide in a disk image.</summary>

1. Open Ubuntu WSL2 and install `curl`, `cryptsetup`, `fdisk`, `tar` and `xz`.
If you intend to use the GUI installer, also make sure `x11-xserver-utils` and `zenity` packages are installed.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar x11-xserver-utils xz zenity`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/<your_username>/Downloads`
  
3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`
  
4. Launch Linuxloops install

- If your WSL version supports GUI applications, you can use the GUI installer by running:

`sudo bash ./linuxloops`

Follow the installer menu, choosing the distro, desktop environment, image path... (the image has to be installed on a NTFS or exfat partition ouside of the WSL VM such as: /mnt/c/Users/<your_username>/linuxloops/distro.img or /mnt/d/linuxloops/distro.img)

- Otherwise using the command line:

Linuxloops arguments description:  
"-distro <distribution>": selects the linux distro (mandatory).  
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is usually selected by default).  
"-dst <path>": destination is the image path such as "/mnt/c/Users/<your_username>/linuxloops/distro.img" (mandatory).  
"-s" <number>: size of the disk image in GB (optional, 14GB by default).  
"-z" <number>: size of the swap (optional) (optional, no swap by default).  
"-e": enable rootfs and swap encryption (optional but highly recommended).  
"-n": automatically install the latest nvidia proprietary driver (optional).  
"-S": automatically apply Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default) (optional).  

As an example `sudo bash ./linuxloops -distro ubuntu -env kde-full -dst /mnt/c/Users/<your_username>/linuxloops/distro.img -s 24 -z 4 -e` will install ubuntu with the complete kde environment a disk image located at path "C:\Users\<your_username>\linuxloops\distro.img" of 24GB size out of which 4GB are dedicated to swap and with an encrypted rootfs/swap.

5. Install and open Grub2Win, click on "Manage Boot Menu" -> "Add a new entry" -> set "Type" as "Create user section", open the file C:\Users\<your_username>\linuxloops\distro.img.grub.txt and copy its content in the Grub2Win notepad window, save and close the Grub2Win notepad window then click "Apply" and "OK".

6. Reboot your computer and start the LinuxLoops grub entry from Grub2Win menu.

</details>

## What to do after installation
- Set-up your language and timezone (refer to the chosen distro's online resources)
- Create additional users if needed.
- Get familiar with the package manager of the distro you have installed (refer to the chosen distro's online resources) and install your favorite software.

In case you run into issues while installing or using LinuxLoops, support is provided currently provided in the off-topic channel of the brunch Discord:

[![Discord][discord-shield]][discord-url]

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
