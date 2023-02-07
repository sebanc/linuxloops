<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guide -->
# Installation from Linux

Linuxloops can install distros on drives or inside disk images.

## Installation on a drive (hdd, sdcard, usb)

### Requirements
- x86_64 based computer with UEFI BIOS.
- Administrator access.
- A drive with at least 14 GB available space.

### Install guide

<details>
  <summary>Click here to open the LinuxLoops install guide  on a drive (hdd, sdcard, usb).</summary>

1. Make sure `btrfs-progs`, `cryptsetup`, `curl`, `dosfstools`, `fdisk`, `tar` and `xz` binaries are installed.
If you intend to use the GUI installer, also make sure `zenity` package is installed.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`
  
4. Launch Linuxloops install

- To use the GUI installer, run:

`sudo bash ./linuxloops`

Follow the installer menu choosing the distro, desktop environment, destination drive...

- Otherwise using the command line:

Linuxloops arguments description:  
"-distro <distribution>": selects the linux distro (mandatory).  
"-env <desktop_environment>": selects the default desktop environment (optional, otherwise gnome is usually selected by default).  
"-dst <path>": destination is the target drive such as "/dev/sdX" (mandatory).  
"-s" <number>: size of the install on drive in GB (optional, if not specified the full disk size is used).  
"-z" <number>: size of the swap (optional) (optional, no swap by default).  
"-b": use btrfs format for the root filesystem (instead of ext4)  
"-e": enable rootfs and swap encryption (optional but highly recommended).  
"-n": automatically install the latest nvidia proprietary driver (optional).  
"-S": automatically apply Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default) (optional).  

As an example `sudo bash ./linuxloops -distro ubuntu -env kde-full -dst /dev/sdX -s 24 -z 4 -e` will install ubuntu with the complete kde environment on the drive /dev/sdX taking 24GB of storage (the remaining space is unallocated) out of which 4GB are dedicated to swap and with an encrypted rootfs/swap.

5. Once install is complete, reboot your computer and choose your drive in the UEFI BIOS boot menu.

6. (Secure Boot enabled) You should see a blue screen, select "Enroll key from disk" -> EFI -> MOK.DER, confirm and reboot your computer.

</details>

## Installation in a disk image

### Requirements
- x86_64 based computer with UEFI BIOS.
- Administrator access.
- 14 GB available space on an unencrypted ext4, exfat or ntfs partition.
- GRUB as Linux distro bootloader.

### Install guide

<details>
  <summary>Click here to open the LinuxLoops install guide in a disk image.</summary>

1. Make sure `btrfs-progs`, `cryptsetup`, `curl`, `dosfstools`, `fdisk`, `tar` and `xz` binaries are installed.
If you intend to use the GUI installer, also make sure `zenity` package is installed.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops`

4. Create a directory for linuxloops images on an unencrypted partition (in ext4, exfat or ntfs format).

As an example `mkdir ~/linuxloops` will create a LinuxLoops directory within the user account path.
  
5. Launch Linuxloops install

- To use the GUI installer, run:

`sudo bash ./linuxloops`

Follow the installer menu choosing the distro, desktop environment, image path... (in this example the image path would be /home/username/linuxloops).

- Otherwise using the command line:

Linuxloops arguments description:  
"-distro <distribution>": selects the linux distro (mandatory).  
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is usually selected by default).  
"-dst <path>": destination is the image path such as "~/linuxloops/distro.img" (mandatory).  
"-s" <number>: size of the disk image in GB (optional, 14GB by default).  
"-z" <number>: size of the swap (optional) (optional, no swap by default).  
"-b": use btrfs format for the root filesystem (instead of ext4)  
"-e": enable rootfs and swap encryption (optional but highly recommended).  
"-n": automatically install the latest nvidia proprietary driver (optional).  
"-S": automatically apply Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default) (optional).  

As an example `sudo bash ./linuxloops -distro ubuntu -env kde-full -dst ~/linuxloops/ubuntu.img -s 24 -z 4 -e` will install ubuntu with the complete kde environment a disk image located at path "~/linuxloops/ubuntu.img" of 24GB size out of which 4GB are dedicated to swap and with an encrypted rootfs/swap.

6. Create a the grub configuration needed to boot the image.

`cat /etc/grub.d/40_custom <image_path>.grub.txt | sudo tee /etc/grub.d/99_linuxloops`

According to the previous example:

`cat /etc/grub.d/40_custom ~/linuxloops/ubuntu.img.grub.txt | sudo tee /etc/grub.d/99_linuxloops`

7. Commit the new entries to Grub.

`sudo grub-mkconfig -o /boot/grub/grub.cfg`

8. (Secure Boot enabled) Enroll the Secure Boot DER certificate.

`sudo mokutil --import ~/linuxloops/ubuntu.img.der`

Choose a password, reboot your computer, you should see a blue screen, select "Enroll MOK" and validate with your chosen password.

9. Reboot your computer and start the LinuxLoops grub entry from your distro's grub menu.

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

