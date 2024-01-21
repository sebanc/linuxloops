<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

# LinuxLoops

## About This Project

Linuxloops is a flexible linux distro installer.  

Why create a custom linux distro installer ?  
Linux is very modular thanks to package management systems, however most distribution installers are either completely manual or focus on a specific DE and bring lots of packages that are not necessarily needed. Linuxloops allows to have minimal installs with more DE options, the possibility to directly include custom packages, Secure Boot support, nvidia proprietary drivers or Linux-surface patches.  
In addition, Linuxloops supports installing linux distros in disk image files that can be booted natively by the GRUB bootloader (from btrfs, ext4, exfat or ntfs partitions) or in VMs.  

The main limitation of Linuxloops is that the partitionning is not currently customizable (EFI, BOOT and ROOT partitions). As such, it is not aimed at users needing complex partition tables (or they can customize the linuxloops script to their liking).  


## How does it work ?

The LinuxLoops script will chroot into a temporary rootfs image (usually linux containers rootfs or an actual distribution iso) and then perform the install from there using the target distribution package manager.  

For security purpose, Linuxloops will not install packages/binaries that are not present in the official distribution repositories. The only exceptions are:  
- The "RPM fusion" repo for Fedora and the "EPEL" repo for RedHat based distros are enabled by default as they contain necessary packages for standard use.  
- For Arch based distros, the "shim-signed" AUR package is included in order to support Secure Boot.  


## Supported Hardware

✔ Base Requirements:  
- x86_64 based computer with UEFI BIOS.  
- Administrative privileges on the device.  
- A drive with at least 14 GB available space.  


## Overview of supported distros and features

|**Distro**|**Version**|**Secure Boot support**|**Nvidia proprietary driver support**|**Linux-surface patches support**|**Notes**|
|----------------|:--------------:|:---------------------:|:-----------------------------------:|:-------------------------------:|--------------|
|AlmaLinux       |9               |✓                      |                                     |                                 |[notes][AlmaLinux-notes]|
|Arch            |Current         |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Arch-notes]|
|Artix           |Current         |✓ (shim-signed AUR)    |✓                                    |                                 |[notes][Artix-notes]|
|BlissOS         |14 / 15         |                       |                                     |                                 |              |
|Brunch          |Latest          |✓                      |                                     |✓ (partially included)           |[notes][Brunch-notes]|
|ChromeOS-Flex   |Latest          |✓                      |                                     |                                 |[notes][ChromeOS-Flex-notes]|
|Debian          |Bookworm        |✓                      |✓                                    |✓                                |              |
|Devuan          |Daedalus        |✓                      |✓                                    |                                 |              |
|Elementary      |7               |✓                      |✓                                    |✓                                |              |
|Fedora          |39              |✓                      |✓                                    |✓                                |[notes][Fedora-notes]|
|Gentoo          |Current         |✓                      |✓                                    |                                 |              |
|Kali            |Current         |disk images only       |✓                                    |✓                                |[notes][Kali-notes]|
|Linuxmint       |Virginia        |✓                      |✓                                    |✓                                |              |
|LMDE            |Faye            |✓                      |✓                                    |✓                                |              |
|Manjaro         |Current         |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Manjaro-notes]|
|MX              |23              |✓                      |✓                                    |✓                                |              |
|Neon            |Current         |✓                      |✓                                    |✓                                |              |
|NixOS           |23.11           |✓                      |✓                                    |                                 |[notes][NixOS-notes]|
|Nobara          |39              |✓                      |✓                                    |✓                                |              |
|OpenSUSE        |Tumbleweed      |✓                      |✓                                    |                                 |[notes][OpenSUSE-notes]|
|Parrot          |Current         |disk images only       |✓                                    |✓                                |[notes][Parrot-notes]|
|Pop             |22.04           |✓                      |✓                                    |✓                                |              |
|Proxmox         |VE 8.0          |✓                      |✓                                    |✓                                |              |
|Qubes           |4.2             |                       |                                     |                                 |[notes][Qubes-notes]|
|RockyLinux      |9               |✓                      |                                     |                                 |[notes][RockyLinux-notes]|
|SteamOS         |3.5             |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][SteamOS-notes]|
|Tails           |Latest          |✓                      |                                     |                                 |[notes][Tails-notes]|
|Ubuntu          |23.10           |✓                      |✓                                    |✓                                |              |
|Ubuntu-LTS      |22.04           |✓                      |✓                                    |✓                                |              |
|Void            |Current         |                       |✓                                    |                                 |              |
|Zorin           |17              |✓                      |✓                                    |✓                                |              |


## Quick start

Linuxloops can be used from any Linux distribution or from Windows WSL, it has limited dependencies that are generally installed by default (most notably `curl`, `tar`, `xz`).  
Note: Windows WSL does not allow to write directly to a disk but you can create images and flash them to a drive using Rufus/Etcher or boot them from [Grub2Win][Grub2Win link].  

Download the linuxloops script:  
`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -o ~/linuxloops`  

### GUI installer

Install the `zenity` package for your distro:  
- Debian-based distro: `sudo apt install zenity`  
- Arch-based distro: `sudo pacman -S zenity`  
- Fedora-based distro: `sudo dnf install zenity`  

Start the installer in GUI mode:  
`sudo bash ~/linuxloops`  


### CLI installer

Below is the list of command line flags:  
```
Usage: sudo bash linuxloops -distro <distribution name> -env <desktop environment> -dst <disk name or disk image path> [-s <total install size>] [-z <swap size>] [-b] [-e] [-L <locale>] [-K <keymap>] [-T <timezone>] [-n] [-S] [-c <custom_packages_list>] [-C <custom_script_path>] [-k <kernel_parameters_list>]
-distro, --distribution <distribution name>			(Distribution to install)
-env, --environment <desktop environment>			(Desktop environment to install)
-dst, --destination <disk name or disk image path>		(e.g. /dev/sda or /ubuntu.img)
-s, --size <total install size>					(number in GB, minimum 14GB)
-z, --swapsize <swap size>					(number in GB)
-b, --btrfs							(Use btrfs for the root filesystem)
-e, --encrypt							(Encrypt the root filesystem)
-L, --locale <locale>						(specify locale to be used, by default "en_US")
-K, --keymap <keymap>						(specify keymap to be used, by default "us")
-T, --timezone <timezone>					(specify timezone to be used, by default "UTC")
-n, --nvidia							(Install nvidia drivers)
-S, --surface							(Add patches for Surface devices from github.com/linux-surface)
-c, --custom-packages						(list of additional packages to be installed - space separated)
-C, --custom-script						(bash script that should be run at the end of the install process)
-k, --kernel-parameters						(specific kernel parameters to be applied - space separated)
-l, --list							(List available distros and desktop environments)
-ll, --list-locales						(List available locales)
-lk, --list-keymaps						(List available keymaps)
-lt, --list-timezones						(List available timezones)
-h, --help							(Display this menu)
```

The only mandatory parameters are: the distribution, the environment and the destination. Use the below command to list available distributions and environments:  
`sudo bash ~/linuxloops -l`  

As an example:  
`sudo bash ~/linuxloops -distro Ubuntu -env Plasma/Full -dst /dev/sdX -e` will install Ubuntu with the complete kde environment on the drive /dev/sdX with encryption.  
`sudo bash ~/linuxloops -distro Arch -env Cinnamon -dst /home/username/arch.img -s 30 -S` will install Arch with the cinnamon desktop environment with the linux-surface patches in a 30 GB image located at /home/username/arch.img.  


## Complementary instructions

### [Detailled instructions to install from Linux][linux-guide]
### [Detailled instructions to install from Windows][windows-guide]
### [Using the Linuxloops Live image][live-image]
### [Use a disk image in a virtual machine][vm-guide]
### [Data recovery from an image][recovery-guide]
### [Recommended setups][recommended-setups]
### [Secure Boot][secure-boot]


## Support

Currently, support for LinuxLoops is provided in the off-topic channel of the brunch Discord:  

[![Discord][discord-shield]][discord-url]


## Special Thanks

- The [linuxcontainers][linuxcontainers link] project for maintaining Linux container rootfs archives.  
- The [Grub2Win][Grub2Win link] project for allowing the GRUB bootloader to be installed on devices running Windows.  
- The [Linux-Surface crew][linux-surface link] for greatly improving Linux support on Surface devices.  


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

<!-- Internal Links -->
[AlmaLinux-notes]: ./Readme/Distro-notes.md#AlmaLinux
[Arch-notes]: ./Readme/Distro-notes.md#Arch
[Artix-notes]: ./Readme/Distro-notes.md#Artix
[Brunch-notes]: ./Readme/Distro-notes.md#Brunch
[ChromeOS-Flex-notes]: ./Readme/Distro-notes.md#ChromeOS-Flex
[Fedora-notes]: ./Readme/Distro-notes.md#Fedora
[Kali-notes]: ./Readme/Distro-notes.md#Kali
[Manjaro-notes]: ./Readme/Distro-notes.md#Manjaro
[NixOS-notes]: ./Readme/Distro-notes.md#NixOS
[OpenSUSE-notes]: ./Readme/Distro-notes.md#OpenSUSE
[Parrot-notes]: ./Readme/Distro-notes.md#Parrot
[Qubes-notes]: ./Readme/Distro-notes.md#Qubes
[RockyLinux-notes]: ./Readme/Distro-notes.md#RockyLinux
[SteamOS-notes]: ./Readme/Distro-notes.md#SteamOS
[Tails-notes]: ./Readme/Distro-notes.md#Tails

[linux-guide]: ./Readme/Install-with-linux.md
[windows-guide]: ./Readme/Install-with-windows.md
[live-image]: ./Readme/Live-image.md
[vm-guide]: ./Readme/Virtual-machines.md
[recovery-guide]: ./Readme/Data-recovery.md
[recommended-setups]: ./Readme/Recommended-setups.md
[secure-boot]: ./Readme/Secure-boot.md

<!-- Outbound Links -->
[Grub2Win link]: https://sourceforge.net/projects/grub2win/
[linuxcontainers link]: https://linuxcontainers.org/
[linux-surface link]: https://github.com/linux-surface/linux-surface

