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

Linuxloops is a generic / declarative linux distribution installer that also supports installing linux distributions in disk image files which can be booted natively by the GRUB bootloader (from btrfs, ext4, exfat or ntfs partitions) or in VMs.  

## Supported hardware

✔ Base Requirements:  
- x86_64 based computer with UEFI BIOS.  
- Administrative privileges on the device.  
- A drive or partition with at least 14 GB available space.  
- For native booting of disks images: A GRUB bootloader installed (or you can use the linuxloops live image one).  

## Quick start (GUI installer)

### Install a linux distro to your HDD

Linuxloops GUI installer can be run from most linux ditributions live images as long as they provide a desktop environment (according to the instructions in the next section), however the available space is often limited in live images and some distros (Bazzite, BlissOS, Brunch, ChromeOS-Flex, Fedora-Atomic, Qubes, Tails) will not be installable due to the lack of storage. As such, it is recommended to use the linuxloops live disk instead.  

* Download the linuxloops live 7z archive in the release section of this Github repository, extract it with your archive manager and write it to a USB flashdrive using an image writer (Gnome Disk Utility / KDE ISO Image Writer for Linux or Rufus for Windows).  

* Reboot your computer and select the USB flashdrive from the UEFI boot menu.  

* If Secure Boot is enabled, you will see the blue shim screen, select "Enroll key from disk" -> EFI -> Debian.der, confirm and reboot your computer.  

* Once the live image has booted, set your keyboard layout (Preferences -> Keyboard -> Layout), connect to WiFi if needed and launch the "Linuxloops installer" from the desktop icon.  

Detailed instructions:  
[Using the Linuxloops Live image][live-image]  

### Install a linux distro on a USB flashdrive / SD card or in a disk image (from Linux or Windows WSL)

Note: Windows WSL does not allow to write directly to a disk but you can create disk images and write them to a USB flashdrive / SD card using Rufus/Etcher or boot them using [Grub2Win][Grub2Win link].  

* Install the below packages depending on your distribution:  
  * Debian / Ubuntu based distributions: `sudo apt install curl fontconfig libasound2t64 libatomic1 libnss3 libxcb-cursor0 libxcb-ewmh2 libxcb-icccm4 libxcb-keysyms1 libxcb-shape0 libxkbcommon-x11-0 libxkbfile1 python3-venv xz-utils`  
  * Arch based distributions: `sudo pacman -Syu curl fontconfig libxkbcommon-x11 nss python-virtualenv xcb-util-cursor xcb-util-keysyms xcb-util-wm xz`  
  * RHEL based distributions: `sudo dnf install curl fontconfig libatomic libxkbcommon-x11 nss python-virtualenv xcb-util-cursor xcb-util-keysyms xcb-util-wm xz`  
  * Gentoo: `sudo emerge app-arch/xz-utils dev-lang/python dev-libs/nss media-libs/fontconfig net-misc/curl x11-libs/libxkbcommon x11-libs/xcb-util-cursor x11-libs/xcb-util-keysyms x11-libs/xcb-util-wm`  
  * OpenSUSE: `sudo zypper in curl fontconfig libatomic1 libgthread-2_0-0 libxcb-cursor0 libxcb-ewmh2 libxcb-keysyms1 libxcb-icccm4 libxcb-shape0 libxkbcommon-x11-0 libxkbfile1 mozilla-nss python3-virtualenv xz`  
  * Void: `sudo xbps-install curl fontconfig libxkbcommon nss xcb-util-cursor xcb-util-keysyms xcb-util-wm xz`  
  * NixOS: No packages to install (the necessary packages will be installed by linuxloops for use in nix-shell environment)  

* Download the Linuxloops script:  
`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -O --create-dirs --output-dir ~/bin`  

* Start linuxloops in GUI mode:  
`bash ${HOME}/bin/linuxloops`  

Detailed instructions:  
[Detailed instructions to install from Linux][linux-guide]  
[Detailed instructions to install from Windows][windows-guide]  

### Support

Support for Linuxloops is provided in the dedicated section of the Brunch Discord server:  
[![Discord][discord-shield]][discord-url]  


## Overview of supported distributions and features

|**Distribution**|**Versions**|**Secure Boot support**|**Nvidia proprietary driver support**|**Linux-surface patches support**|**Notes**|
|----------------|:------------------------------------------------------------:|:---------------------:|:-----------------------------------:|:-------------------------------:|----------------------------|
|AlmaLinux       |9                                                             |✓                      |                                     |                                 |                            |
|Arch            |Stable<br>Testing                                             |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Arch-notes]         |
|Artix           |Openrc<br>Runit<br>S6<br>Dinit<br>(Stable<br>or<br>Testing)   |✓ (shim-signed AUR)    |✓                                    |                                 |[notes][Artix-notes]        |
|Bazzite         |Stable<br>Testing<br>Unstable                                 |✓ (shim-signed AUR)    |✓                                    |                                 |[notes][Bazzite-notes]      |
|BlendOS         |v4                                                            |✓ (shim-signed AUR)    |✓                                    |                                 |[notes][BlendOS-notes]      |
|BlissOS         |15<br>16                                                      |                       |                                     |                                 |                            |
|Brunch          |Stable<br>Unstable                                            |✓                      |                                     |✓                                |[notes][Brunch-notes]       |
|CachyOS         |x86-64<br>x86-64-v3<br>x86-64-v4                              |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][CachyOS-notes]      |
|ChromeOS-Flex   |Stable                                                        |✓                      |                                     |                                 |[notes][ChromeOS-Flex-notes]|
|Debian          |Bookworm<br>Testing<br>Unstable                               |✓                      |✓                                    |✓                                |                            |
|Devuan          |Daedalus<br>Testing                                           |✓                      |✓                                    |                                 |                            |
|Elementary      |8                                                             |✓                      |✓                                    |✓                                |                            |
|Fedora          |41<br>Rawhide                                                 |✓                      |✓                                    |✓                                |[notes][Fedora-notes]       |
|Fedora-Atomic   |41<br>Rawhide                                                 |✓                      |✓                                    |                                 |[notes][Fedora-Atomic-notes]|
|Gentoo          |23/Openrc<br>23/Systemd                                       |✓                      |✓                                    |                                 |                            |
|GLF-OS          |Stable                                                        |✓                      |✓                                    |                                 |                            |
|Kali            |Rolling                                                       |disk images only       |✓                                    |✓                                |[notes][Kali-notes]         |
|KDE             |Rolling                                                       |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][KDE-notes]          |
|Linuxmint       |Xia                                                           |✓                      |✓                                    |✓                                |                            |
|LMDE            |Faye                                                          |✓                      |✓                                    |✓                                |                            |
|Manjaro         |Stable<br>Testing<br>Unstable                                 |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][Manjaro-notes]      |
|MX              |23                                                            |✓                      |✓                                    |✓                                |                            |
|Neon            |User<br>Testing                                               |✓                      |✓                                    |✓                                |                            |
|NixOS           |24.11<br>Unstable                                             |✓                      |✓                                    |                                 |                            |
|Nobara          |41                                                            |✓                      |✓                                    |✓                                |                            |
|OpenSUSE        |Leap/15.6<br>Slowroll<br>Tumbleweed                           |✓                      |✓                                    |                                 |[notes][OpenSUSE-notes]     |
|Parrot          |Lory                                                          |disk images only       |✓                                    |                                 |[notes][Parrot-notes]       |
|PikaOS          |Nest                                                          |✓                      |✓                                    |                                 |                            |
|Pop             |22.04<br>24.04                                                |✓                      |✓                                    |✓                                |                            |
|Proxmox         |VE8                                                           |✓                      |✓                                    |✓                                |                            |
|Qubes           |4.2.3                                                         |                       |                                     |                                 |[notes][Qubes-notes]        |
|RockyLinux      |9                                                             |✓                      |                                     |                                 |                            |
|SteamOS         |3.6                                                           |✓ (shim-signed AUR)    |✓                                    |✓                                |[notes][SteamOS-notes]      |
|Tails           |Stable                                                        |✓                      |                                     |                                 |[notes][Tails-notes]        |
|Ubuntu          |24.04<br>24.10<br>25.04                                       |✓                      |✓                                    |✓                                |                            |
|Void            |Current                                                       |                       |✓                                    |                                 |                            |
|Zorin           |17                                                            |✓                      |✓                                    |✓                                |                            |


## About this project

Why create a linux distribution installer ?  
Linux is very modular thanks to package management systems, however most distribution installers are either completely manual or focus on a specific DE and bring lots of packages that are not necessarily needed. Linuxloops allows minimal Linux installs with more DE options, to directly add custom packages, Secure Boot support, nvidia proprietary drivers or Linux-surface patches.  


## How does it work ?

The Linuxloops script will chroot into a temporary rootfs image (usually a linux container rootfs or an actual distribution iso) and then perform the install from there using the target distribution package manager.  

Linuxloops can be used from any Linux distribution or from Windows WSL, it has limited dependencies that are installed by default in most if not all Linux distros: bash, coreutils, curl, grep, sed, sudo, tar, util-linux, xz.  

For security purpose, Linuxloops will not install packages/binaries that are not present in the official distribution repositories. The only exceptions are:  
- The "RPM fusion" repo for Fedora and the "EPEL" repo for RedHat based distributions that are enabled by default as they contain necessary packages for standard use.  
- For Arch based distributions, the "shim-signed" AUR package is included in order to support Secure Boot.  


## Other install methods

### CLI mode

Install the `curl` package for your distribution and download the Linuxloops script:  
`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -O --create-dirs --output-dir ~/bin`  

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

Install the `curl` package for your distribution and download the Linuxloops script:  
`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -O --create-dirs --output-dir ~/bin`  

Have a look at the declarative configuration examples available here:  
[Declarative configuration examples][Declarative configuration examples]  

The main parameters are: the distribution, the version and the environment. Use the below command to list available distributions and environments:  
`bash ${HOME}/bin/linuxloops -l`  

Create your own declarative configuration and run the below command to start the install:  
`bash ${HOME}/bin/linuxloops -d <path_to_your_declarative_configuration>`  

### Detailed instructions
[Detailed instructions to install from Linux][linux-guide]  
[Detailed instructions to install from Windows][windows-guide]  
[Using the Linuxloops Live image][live-image]  
[Use a disk image in a virtual machine][vm-guide]  
[Data recovery from an image][recovery-guide]  
[Recommended setups][recommended-setups]  
[Secure Boot][secure-boot]  

### Support

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
[Arch-notes]: ./Readme/Distro-notes.md#Arch
[Artix-notes]: ./Readme/Distro-notes.md#Artix
[Bazzite-notes]: ./Readme/Distro-notes.md#Bazzite
[BlendOS-notes]: ./Readme/Distro-notes.md#BlendOS
[Brunch-notes]: ./Readme/Distro-notes.md#Brunch
[CachyOS-notes]: ./Readme/Distro-notes.md#CachyOS
[ChromeOS-Flex-notes]: ./Readme/Distro-notes.md#ChromeOS-Flex
[Fedora-notes]: ./Readme/Distro-notes.md#Fedora
[Fedora-Atomic-notes]: ./Readme/Distro-notes.md#Fedora-Atomic
[Kali-notes]: ./Readme/Distro-notes.md#Kali
[KDE-notes]: ./Readme/Distro-notes.md#KDE
[Manjaro-notes]: ./Readme/Distro-notes.md#Manjaro
[OpenSUSE-notes]: ./Readme/Distro-notes.md#OpenSUSE
[Parrot-notes]: ./Readme/Distro-notes.md#Parrot
[Qubes-notes]: ./Readme/Distro-notes.md#Qubes
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

