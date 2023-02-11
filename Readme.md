<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

# LinuxLoops (beta)

## About This Project

Linuxloops is a custom linux distro installer.

Why create a custom linux distro installer ?
Most linux distros provide installers which are either focused on a specific DE and bloated with software you don't need or completely manual. Moreover, once installed there are very often specific pain points to have a fully working system (generally needed config files, declarative configurations, dkms drivers signing for secure boot...).

The objective of Linuxloops is to:
- Allow an easy installation of a choosen linux distro with full hardware support OOTB, the desktop environment of your choice, and either minimal apps (file manager and terminal when possible) or full standard distro installer packages depending on the choosen target (aside from predefined targets, you can also include additional packages or use a custom install script, see "Custom install" section).
- In addition, Linuxloops supports installing linux distros in disk image files which can be booted natively from the GRUB bootloader (only on btrfs, ext4, exfat or ntfs partitions) or in VMs.

On the other hand, the main limitation of Linuxloops is that in order to support a wide range of Linux distros, the partition table setup is limited to the basics (EFI partition and BOOT/ROOT ext4 partitions). As such, most advanced users needing a custom partition table would probably be better with a distro netinst iso or can customize the linuxloops script to their liking (it is just a bash script).

## How does it work ?

The LinuxLoops bash script will create a standard partition table (with a 512MB EFI partition, a 1.5GB boot partition and the main rootfs partition), download rootfs images (usually lxc container rootfs or actual distribution isos) and install the necessary packages through a chroot process.

For security purpose, Linuxloops will not install packages/binaries which are not present in the official repositories. The only exceptions are:
- The "RPM fusion" repo for Fedora and the "EPEL" repo for RedHat derivatives which are enabled by default as they contain necessary packages for standard use.
- For archlinux derivatives, the "shim-signed" AUR package in order to support Secure Boot.

The minimum size for a LinuxLoops image has been defined as 14GB (with at least 12GB allocated to the main rootfs) as it should allow most distros to install without issue. However, it might not be sufficient for all distros, notably if you intend to install gentoo with a desktop environment you will most likely need 40 GB minimum for the main rootfs (as it needs a lot of disk space to build everything from source).

**Warning: Even though, if something goes wrong with your install you should always be able to recover your data by mounting the root partition from a Linux live usb (see Data recovery section), make sure to keep regular backups of your data and keep in mind that this software is provided as is without any guarantee of any kind.**


## Supported Hardware

✔ Base Requirements:
- x86_64 based computer with UEFI BIOS.
- Administrative privileges on the device.


## Overview of supported distros and features

|**Distro**|**Swap support**|**Encryption support**|**Secure Boot support**|**Nvidia proprietary driver support**|**Linux-surface patches support**|**Others**|
|--------------|:--------------:|:--------------------:|:---------------------:|:-----------------------------------:|:-------------------------------:|--------------|
|almalinux     |✓               |✓                     |✓                      |                                     |                                 |[almalinux notes][almalinux-notes]|
|archlinux     |✓               |✓                     |✓ (shim-signed AUR)    |✓                                    |✓                                |[archlinux notes][archlinux-notes]|
|artixlinux    |✓               |✓                     |✓ (shim-signed AUR)    |✓                                    |                                 |[artixlinux notes][artixlinux-notes]|
|brunch        |                |✓ (distro specific)   |✓                      |                                     |✓ (partially included)           |[brunch notes][brunch-notes]|
|chromeos-flex |                |✓ (distro specific)   |✓                      |                                     |                                 |[chromeos-flex notes][chromeos-flex-notes]|
|debian        |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|devuan        |✓               |✓                     |✓                      |✓                                    |                                 |              |
|elementary    |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|fedora        |✓               |✓                     |✓                      |✓                                    |✓                                |[fedora notes][fedora-notes]|
|gentoo-openrc |✓               |✓                     |disk images only       |✓                                    |                                 |[gentoo-openrc notes][gentoo-notes]|
|gentoo-systemd|✓               |✓                     |disk images only       |✓                                    |                                 |[gentoo-systemd notes][gentoo-notes]|
|kali          |✓               |✓                     |disk images only       |✓                                    |✓                                |[kali notes][kali-notes]|
|kde_neon      |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|manjaro       |✓               |✓                     |✓ (shim-signed AUR)    |✓                                    |✓                                |[manjaro notes][manjaro-notes]|
|mint          |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|mint-lmde     |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|mxlinux       |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|nixos         |✓               |✓                     |disk images only       |✓                                    |                                 |[nixos notes][nixos-notes]|
|opensuse      |✓               |✓                     |✓                      |✓                                    |                                 |[opensuse notes][opensuse-notes]|
|parrot        |✓               |✓                     |disk images only       |✓                                    |✓                                |[parrot notes][parrot-notes]|
|pop_os        |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|rockylinux    |✓               |✓                     |✓                      |                                     |                                 |[rockylinux notes][rockylinux-notes]|
|steamos-like  |✓               |✓                     |✓ (shim-signed AUR)    |✓                                    |✓                                |[steamos-like notes][steamos-like-notes]|
|tails         |                |✓ (distro specific)   |✓                      |                                     |                                 |[tails notes][tails-notes]|
|ubuntu        |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|ubuntu-lts    |✓               |✓                     |✓                      |✓                                    |✓                                |              |
|voidlinux     |✓               |✓                     |                       |✓                                    |                                 |              |
|zorin         |✓               |✓                     |✓                      |✓                                    |✓                                |              |


## Encryption

Encryption is highly recommended as it protects physical access to your personal data.

If selected, Linuxloops will setup encryption on the rootfs (including swap) using LUKS2. However, note that tails and brunch/chromeos-flex have their own encryption mechanism (and that in the case of brunch/chromeos-flex you will not have the necessary key to decrypt userdata from outside chromeos as it is generated by the system so ensure your data is synced on the cloud or make regular backups).
  
By default, after a Linuxloops install the keyboard layout will be in Qwerty, as such:
- Either Learn how to type your password as if your keyboard was Qwerty.
- Or choose a password which is identical when typed on a Qwerty keyboard.


## Install instructions

This guide has been split into seperate sections depending on your current operating system.

### [Install from Linux][linux-guide]
### [Install from Windows][windows-guide]


## Complementary instructions

You will find below additional instructions to go further with Linuxloops.

### [Custom install parameters][custom-guide]
### [Use a disk image in a virtual machine][vm-guide]
### [Data recovery from an image][recovery-guide]
### [Recommended setups][recommended-setups]
### [Secure Boot][secure-boot]


## Support

Currently, support for LinuxLoops is provided in the off-topic channel of the brunch Discord:

[![Discord][discord-shield]][discord-url]


## Pull requests

Clearly, in its current state, LinuxLoops is not perfect and I am counting on the community to help by submitting pull requests, notably to:
- Add new desktop environments / windows managers targets (especially windows managers as I do not have much experience with those).
- Fiabilise the installed packages base for each target.
- Extend Linuxloops customization principles.
- Fix random bugs.

However:
- New linux distros will only be added if they present an effective interest (as Linuxloops is an installer, a distro which would mainly consist of a custom installer and a theme are not considered relevant).
- Changes related to the default partitioning scheme can be discussed, however in order to support a wide range of distros only widely supported filesystems can be considered.

You can also feel free to make your own fork of LinuxLoops and customize it to your needs (it is just a bash script).


## Special Thanks
- The [lxc/lxd][lxc link] project for maintaining Linux container rootfs archives.
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
[almalinux-notes]: ./Readme/Distro-notes.md#almalinux
[archlinux-notes]: ./Readme/Distro-notes.md#archlinux
[artixlinux-notes]: ./Readme/Distro-notes.md#artixlinux
[brunch-notes]: ./Readme/Distro-notes.md#brunch
[chromeos-flex-notes]: ./Readme/Distro-notes.md#chromeos-flex
[fedora-notes]: ./Readme/Distro-notes.md#fedora
[gentoo-notes]: ./Readme/Distro-notes.md#gentoo
[kali-notes]: ./Readme/Distro-notes.md#kali
[manjaro-notes]: ./Readme/Distro-notes.md#manjaro
[nixos-notes]: ./Readme/Distro-notes.md#nixos
[opensuse-notes]: ./Readme/Distro-notes.md#opensuse
[parrot-notes]: ./Readme/Distro-notes.md#parrot
[rockylinux-notes]: ./Readme/Distro-notes.md#rockylinux
[steamos-like-notes]: ./Readme/Distro-notes.md#steamos-like
[tails-notes]: ./Readme/Distro-notes.md#tails

[linux-guide]: ./Readme/Install-with-linux.md
[windows-guide]: ./Readme/Install-with-windows.md

[custom-guide]: ./Readme/Custom-install.md
[vm-guide]: ./Readme/Virtual-Machines.md
[recovery-guide]: ./Readme/Data-recovery.md
[recommended-setups]: ./Readme/Recommended-setups.md
[secure-boot]: ./Readme/Secure-Boot.md

<!-- Outbound Links -->
[lxc link]: https://linuxcontainers.org/
[linux-surface link]: https://github.com/linux-surface/linux-surface
