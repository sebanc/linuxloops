<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guides -->
This guide is for installing LinuxLoops on your computer from Windows using WSL2. There are two variants, you can choose to install Grub2Win software to boot LinuxLoops images directly from HDD or use an USB flashdrive as the LinuxLoops bootloader. 

# Before you start (recommended setup)

Windows locks NTFS partitions when fast startup and hibernation are enabled, therefore the suggested approach to install LinuxLoops from Windows is to use the disk manager to reduce the main storage and create an exfat partition to store images.

Otherwise, you can install LinuxLoops on NTFS partitions but you have to make sure that bitlocker, fast startup and hibernation are disabled (refer to online resources).

# 1st method: Using Grub2Win as bootloader (Boot the image from HDD)

<details>
  <summary>Click to open the LinuxLoops GUI install guide with Grub2Win as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- Windows 11 with Ubuntu WSL2 installed.
- 10 GB available space on an unencrypted partition (bitlocker disabled).
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Open Ubuntu WSL2 and install curl, cryptsetup, fdisk, tar and zenity packages.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar zenity`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/username/Downloads`
  
3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`
  
4. Launch the GUI installer:

`sudo bash linuxloops`

5. Follow the installer menu, choosing the distro, desktop environment, image path... (the image has to be installed on a NTFS or exfat partition ouside of the WSL VM such as: /mnt/c/Users/username/linuxloops/distro.img or /mnt/d/linuxloops/distro.img)

6. Install and open Grub2Win, click on "Manage Boot Menu" -> "Add a new entry" -> set "Type" as "Create user section", open the file <distro>.img.grub.txt and copy its content in the Grub2Win notepad window, save and close the Grub2Win notepad window then click "Apply" and "OK".

7. Reboot your computer and start the LinuxLoops grub entry from Grub2Win menu.

</details>

<details>
  <summary>Click to open the LinuxLoops command line install guide with Grub2Win as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- Windows 11 with Ubuntu WSL2 installed.
- 10 GB available space on an unencrypted partition (bitlocker disabled).
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps
1. Open Ubuntu WSL2 and install curl, cryptsetup, fdisk and tar packages.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/username/Downloads`
  
3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`

4. List available distros and desktop environments:

`sudo bash linuxloops -l`

5. Launch the installer:

Arguments description:
"-dist <distribution>": selects the linux distro (mandatory)
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is generally selected by default)
"-img <path>": set the path to the disk image. The image has to be installed on a NTFS or exfat partition ouside of the WSL VM such as: /mnt/c/Users/username/linuxloops/distro.img or /mnt/d/linuxloops/distro.img (mandatory)
"-s" <number>: size of the disk image in GB (optional, 10GB by default)
"-z" <number>: size of the swap (optional) (optional, no swap by default)
"-e": enable rootfs and swap partitions encryption (optional but highly recommended)
"-S": automatically applied Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default)

`sudo bash linuxloops -dist ubuntu -env kde-full -img /mnt/c/Users/<username>/ubuntu.img -s 24 -z 4 -e`

6. Install and open Grub2Win, click on "Manage Boot Menu" -> "Add a new entry" -> set "Type" as "Create user section", open the file <distro>.img.grub.txt and copy its content in the Grub2Win notepad window, save and close the Grub2Win notepad window then click "Apply" and "OK".

7. Reboot your computer and start the LinuxLoops grub entry from Grub2Win menu.

</details>

# 2nd method: Use an USB flashdrive as bootloader (Boot the image from USB)

<details>
  <summary>Click to open the LinuxLoops GUI install guide with an USB flashdrive as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- Windows 11 with Ubuntu WSL2 installed.
- 10 GB available space on an unencrypted partition (bitlocker disabled).
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Open Ubuntu WSL2 and install curl, cryptsetup, fdisk, tar and zenity packages.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar zenity`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/username/Downloads`
  
3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`

4. Download the USB bootloader template image.

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/usb_bootloader.img`
  
5. Launch the GUI installer:

`sudo bash linuxloops`

6. Follow the installer menu, choosing the distro, desktop environment, image path... (the image has to be installed on a NTFS or exfat partition ouside of the WSL VM such as: /mnt/c/Users/username/linuxloops/distro.img or /mnt/d/linuxloops/distro.img)

7. Install rufus and write usb_bootloader.img file from your Downloads folder to a USB flashdrive.

8. Reboot your computer and select your USB flashdrive as boot device in the BIOS.

</details>

<details>
  <summary>Click to open the LinuxLoops command line install guide with an USB flashdrive as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- Windows 10/11 with Ubuntu WSL2 installed.
- 10 GB available space on an unencrypted partition (bitlocker disabled).
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps
1. Open Ubuntu WSL2 and install curl, cryptsetup, fdisk and tar packages.

`sudo apt update && sudo apt -y install curl cryptsetup fdisk tar`

2. Change the directory to your Windows Downloads folder (replace username with your Windows username).

`cd /mnt/c/Users/username/Downloads`

3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`

4. Download the USB bootloader template image.

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/usb_bootloader.img`
  
5. List available distros and desktop environments:

`sudo bash linuxloops -l`

6. Launch the installer:

Arguments description:
"-dist <distribution>": selects the linux distro (mandatory)
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is generally selected by default)
"-img <path>": set the path to the disk image. The image has to be installed on a NTFS or exfat partition ouside of the WSL VM such as: /mnt/c/Users/username/linuxloops/distro.img or /mnt/d/linuxloops/distro.img (mandatory)
"-s" <number>: size of the disk image in GB (optional, 10GB by default)
"-z" <number>: size of the swap (optional) (optional, no swap by default)
"-e": enable rootfs and swap partitions encryption (optional but highly recommended)
"-S": automatically applied Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default)

`sudo bash linuxloops -dist ubuntu -env kde-full -img /mnt/c/Users/<username>/ubuntu.img -s 24 -z 4 -e`

7. Install rufus and write usb_bootloader.img file from your Downloads folder to a USB flashdrive.

8. Reboot your computer and select your USB flashdrive as boot device in the BIOS.

</details>

### What to do after installation
- Get familiar with the package manager of the distro you have installed (refer to the chosen distro's online resources)
- Set-up your language and timezone (refer to the chosen distro's online resources)
- Create additional users if needed.
- Install your favorite software and enjoy.

In case you run into issues while installing or using LinuxLoops, you can find support in the LinuxLoops section of the brunch discord group:

[![Discord][discord-shield]][discord-url]

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops-beta?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops-beta?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops-beta/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
