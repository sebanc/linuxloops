<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Project Logo -->
<p align="center">
  <a href="https://github.com/sebanc/linuxloops" title="Linuxloops">
   <img src="./linuxloops.png" width="128px" alt="Logo"/>
  </a>
</p>
<h1 align="center">Linuxloops</h1>

## About This Project

Linuxloops is an adaptable / declarative linux distribution installer.  

Why create a linux distribution installer ?  
Linux is very modular thanks to package management systems, however most distribution installers are either completely manual or focus on a specific DE and bring lots of packages that are not necessarily needed. Linuxloops allows minimal Linux installs with more DE options, to directly add custom packages, Secure Boot support, nvidia proprietary drivers or Linux-surface patches.  
In addition, Linuxloops supports installing linux distributions in disk image files that can be booted natively by the GRUB bootloader (from btrfs, ext4, exfat or ntfs partitions) or in VMs.  


## How does it work ?

The Linuxloops script will chroot into a temporary rootfs image (usually a linux container rootfs or an actual distribution iso) and then perform the install from there using the target distribution package manager.  

Linuxloops can be used from any Linux distribution or from Windows WSL, it has limited dependencies that are installed by default in most if not all Linux distros: bash, coreutils, curl, grep, sed, sudo, tar, util-linux, xz.  
Note: Windows WSL does not allow to write directly to a disk but you can create disk images and flash them to a drive using Rufus/Etcher or boot them from [Grub2Win][Grub2Win link].  

For security purpose, Linuxloops will not install packages/binaries that are not present in the official distribution repositories. The only exceptions are:  
- The "RPM fusion" repo for Fedora and the "EPEL" repo for RedHat based distributions that are enabled by default as they contain necessary packages for standard use.  
- For Arch based distributions, the "shim-signed" AUR package is included in order to support Secure Boot.  


## Supported Hardware

✔ Base Requirements:  
- x86_64 based computer with UEFI BIOS.  
- Administrative privileges on the device.  
- A drive or partition with at least 14 GB available space.  


## Overview of supported distributions and features

|**Distribution**|**Versions**|**Secure Boot support**|**Nvidia proprietary driver support**|**Linux-surface patches support**|**Notes**|
|----------------|:------------------------------------------------------------:|:---------------------:|:-----------------------------------:|:-------------------------------:|----------------------------|
|AlmaLinux       |9                                                             |✓                      |                                     |                                 |[notes][AlmaLinux-notes]    |
|Arch            |Current                                                       |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Arch-notes]         |
|Artix           |Current/Openrc<br>Current/Runit<br>Current/S6<br>Current/Dinit|✓ (shim-signed AUR)    |✓                                    |                                 |[notes][Artix-notes]        |
|BlendOS         |v4                                                            |✓ (shim-signed AUR)    |✓                                    |                                 |[notes][BlendOS-notes]      |
|BlissOS         |15<br>16                                                      |                       |                                     |                                 |                            |
|Brunch          |Stable Unstable                                               |✓                      |                                     |✓                                |[notes][Brunch-notes]       |
|CachyOS         |x86-64<br>x86-64-v3<br>x86-64-v4                              |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][CachyOS-notes]      |
|ChimeraOS       |Stable<br>Unstable                                            |✓                      |                                     |                                 |                            |
|ChromeOS-Flex   |Stable                                                        |✓                      |                                     |                                 |[notes][ChromeOS-Flex-notes]|
|Debian          |Bookworm<br>Testing<br>Unstable                               |✓                      |✓                                    |✓                                |                            |
|Devuan          |Daedalus<br>Testing<br>Unstable                               |✓                      |✓                                    |                                 |                            |
|Elementary      |7                                                             |✓                      |✓                                    |✓                                |                            |
|Fedora          |40<br>41<br>Rawhide                                           |✓                      |✓                                    |✓                                |[notes][Fedora-notes]       |
|Gentoo          |23/Openrc<br>23/Systemd                                       |✓                      |✓                                    |                                 |                            |
|Kali            |Rolling                                                       |disk images only       |✓                                    |✓                                |[notes][Kali-notes]         |
|Linuxmint       |Wilma                                                         |✓                      |✓                                    |✓                                |                            |
|LMDE            |Faye                                                          |✓                      |✓                                    |✓                                |                            |
|Manjaro         |Stable<br>Testing<br>Unstable                                 |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Manjaro-notes]      |
|MX              |23                                                            |✓                      |✓                                    |✓                                |                            |
|Neon            |User<br>Testing<br>Unstable                                   |✓                      |✓                                    |✓                                |                            |
|NixOS           |24.05<br>24.11<br>Unstable                                    |✓                      |✓                                    |                                 |                            |
|Nobara          |40                                                            |✓                      |✓                                    |✓                                |                            |
|OpenSUSE        |15.6<br>Tumbleweed                                            |✓                      |✓                                    |                                 |[notes][OpenSUSE-notes]     |
|Parrot          |Lory                                                          |disk images only       |✓                                    |✓                                |[notes][Parrot-notes]       |
|Pop             |22.04<br>24.04                                                |✓                      |✓                                    |✓                                |                            |
|Proxmox         |VE8                                                           |✓                      |✓                                    |✓                                |                            |
|Qubes           |4.2.3                                                         |                       |                                     |                                 |[notes][Qubes-notes]        |
|RockyLinux      |9                                                             |✓                      |                                     |                                 |[notes][RockyLinux-notes]   |
|SteamOS         |3.6                                                           |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][SteamOS-notes]      |
|Tails           |Stable                                                        |✓                      |                                     |                                 |[notes][Tails-notes]        |
|Ubuntu          |24.04<br>24.10<br>25.04                                       |✓                      |✓                                    |✓                                |                            |
|Void            |Current                                                       |                       |✓                                    |                                 |                            |
|Zorin           |17                                                            |✓                      |✓                                    |✓                                |                            |


## Quick start

Download the Linuxloops script:  
`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -O --create-dirs --output-dir ~/bin`  

### GUI mode

Install the `PyQtWebEngine` package for your distribution:  
- Debian / Ubuntu derivatives:  
&nbsp;&nbsp;&nbsp;&nbsp;Debian 12 / Ubuntu 24.04 and above: `sudo apt install python3-venv python3-pyqt6.qtwebengine`  
&nbsp;&nbsp;&nbsp;&nbsp;Older Debian / Ubuntu versions: `sudo apt install python3-venv python3-pyqt5.qtwebengine`  
- Arch-based distributions: `sudo pacman -Syu python-pyqt6-webengine`  
- RHEL-based distributions: `sudo dnf install python3-pyqt6-webengine`  
- OpenSUSE: `sudo zypper in python3-PyQt6-WebEngine`  
- Gentoo: `sudo emerge dev-python/PyQt6-WebEngine`  
- Void: `sudo xbps-install python3-pyqt6-webengine python3-pyqt6-gui python3-pyqt6-widgets python3-pyqt6-network python3-pyqt6-webchannel python3-pyqt6-printsupport`  
- NixOS: No package to install (python3Packages.pyqt6-webengine will be installed by linuxloops in nix-shell environment)  

Once the `PyQtWebEngine` package is installed, start linuxloops in GUI mode:  
`bash ${HOME}/bin/linuxloops`  

### CLI mode

List of command line flags:  
```
Usage: bash ${HOME}/bin/linuxloops -distro <distribution name> -ver <distribution version> -env <environment name> -dst <disk name or disk image path>
-distro, --distribution <distribution name>		(Distribution to install)
-ver, --version <version name>				(Distribution version to install)
-env, --environment <environment name>			(Environment to install)
-dst, --destination <disk name or disk image path>	(e.g. /dev/sda or /ubuntu.img)
-s, --size <total install size>				(number in GB, minimum 14GB)
-z, --swapsize <swap size>				(number in GB)
-b, --btrfs						(Use btrfs for the root filesystem)
-r, --rootfs-compression				(Enable standard btrfs compression, implies -b)
-e, --encrypt						(Encrypt the root filesystem)
-a, --autologin						(Enable user autologin)
    --efi-name						(EFI partition name)
    --efi-mountoptions					(EFI partition specific mountoptions)
    --boot-name						(Boot partition name)
    --boot-mountoptions					(Boot partition specific mountoptions)
    --root-name						(Root partition name)
    --root-mountoptions					(Root partition specific mountoptions)
-A, --add-partition <partition details>			(Add a partition according to the below format:
							<mountpoint>*<name>*<fstype>*<mountoptions>*<size(in GB)>*<encryption>
							ex: /home*Home*ext4*noatime,discard*20*Yes)
-H, --hostname						(Provide a specific hostname)
-L, --locale <locale>					(specify locale to be used, by default "en_US")
-K, --keymap <keymap>					(specify keymap to be used, by default "us")
-T, --timezone <timezone>				(specify timezone to be used, by default "UTC")
-n, --nvidia						(Install nvidia drivers)
-S, --surface						(Add patches for Surface devices from github.com/linux-surface)
-c, --custom-packages					(list of additional packages to be installed - space separated)
-C, --custom-script					(bash script that should be run at the end of the install process)
-k, --kernel-parameters					(specific kernel parameters to be applied - space separated)
-m, --custom-mirror <mirror details>			(Add a custom mirror according to the below format:
							<repository>*<mirror>
							ex: Arch*https://mirrors.kernel.org/archlinux)
-p, --user-password-for-encryption			(Use user account password for encryption)
-g, --grub-hide						(Hide the GRUB Bootloader)
-G, --generate-declarative-config <config_file_path>	(Generate a declarative configuration file)
-d, --apply-declarative-config <config_file_path>	(Use a declarative configuration file)
-l, --list						(List available distributions and environments)
-lb, --list-btrfs					(Confirms if btrfs is supported for chosen distribution/version)
-ld, --list-distributions				(List available distributions)
-le, --list-environments				(List available environments for chosen distribution/version)
-ll, --list-locales					(List available locales)
-lk, --list-keymaps					(List available keymaps)
-ln, --list-nvidia					(Confirms if nvidia proprietary driver is supported for chosen distribution/version)
-ls, --list-surface					(Confirms if Surface devices patches are supported for chosen distribution/version)
-lt, --list-timezones					(List available timezones)
-lv, --list-versions					(List available versions for chosen distribution)
-h, --help						(Display this menu)
```

The main parameters are: the distribution, the version, the environment and the destination. Use the below command to list available distributions, versions and environments:  
`bash ${HOME}/bin/linuxloops -l`  

As an example:  
`bash ${HOME}/bin/linuxloops -distro Ubuntu -ver 24.04 -env Plasma/Full -dst /dev/sdX -e` will install Ubuntu 24.04 with the complete kde environment on the drive /dev/sdX with encryption.  
`bash ${HOME}/bin/linuxloops -distro Arch -ver Current -env Cinnamon -dst ~/arch.img -s 30 -S` will install Arch with the cinnamon desktop environment and linux-surface patches in a 30 GB image located at /home/username/arch.img.  

### Declarative mode

Have a look at the declarative configuration examples available here:  
[Declarative configuration examples][Declarative configuration examples]  

The main parameters are: the distribution, the version and the environment. Use the below command to list available distributions and environments:  
`bash ${HOME}/bin/linuxloops -l`  

Create your own declarative configuration and run the below command to start the install:  
`bash ${HOME}/bin/linuxloops -d <path_to_your_declarative_configuration>`  

## Complementary instructions

### [Detailed instructions to install from Linux][linux-guide]
### [Detailed instructions to install from Windows][windows-guide]
### [Using the Linuxloops Live image][live-image]
### [Use a disk image in a virtual machine][vm-guide]
### [Data recovery from an image][recovery-guide]
### [Recommended setups][recommended-setups]
### [Secure Boot][secure-boot]


## Support

Support for Linuxloops is provided in the dedicated section of the Brunch Discord server:  

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
[BlendOS-notes]: ./Readme/Distro-notes.md#BlendOS
[Brunch-notes]: ./Readme/Distro-notes.md#Brunch
[CachyOS-notes]: ./Readme/Distro-notes.md#CachyOS
[ChromeOS-Flex-notes]: ./Readme/Distro-notes.md#ChromeOS-Flex
[Fedora-notes]: ./Readme/Distro-notes.md#Fedora
[Kali-notes]: ./Readme/Distro-notes.md#Kali
[Manjaro-notes]: ./Readme/Distro-notes.md#Manjaro
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
[Declarative configuration examples]: ./Declarative_configuration_examples

<!-- Outbound Links -->
[Grub2Win link]: https://sourceforge.net/projects/grub2win/
[linuxcontainers link]: https://linuxcontainers.org/
[linux-surface link]: https://github.com/linux-surface/linux-surface

