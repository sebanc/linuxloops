<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

# LinuxLoops (beta)

<!-- About This Project -->
## About This Project

The purpose of LinuxLoops script is to install full linux x86_64 distros into disk images from Linux, Windows (WSL2) or ChromeOS (brunch singleboot / chromebook with dev mode + RW_LEGACY firmware).

Supported setups:  
|**OS used for Installation**|**supported fs for image**|**bootloader**|
|----------------------------|--------------------------|---------------|
|Linux                       |ext4 ntfs exfat           |Linux distro grub or usb flashdrive|
|Windows (WSL2)              |ntfs exfat                |Grub2Win or usb flashdrive|
|Brunch singleboot           |ext4                      |Brunch grub or usb flashdrive|
|ChromeOS                    |ext4                      |Grub installed by linuxloops or usb flashdrive|

Currently the below distros are supported:  
|**Distro**|**Swap support**|**Encryption support**|**Linux-surface patches support**|**Specific notes**|
|archlinux|✓|✓|✓||
|debian|✓|✓|✓||
|elementary|✓|✓|✓||
|fedora|✓|✓|✓||
|gentoo|✓|✓|||
|kali|✓|✓|✓||
|manjaro|✓|✓|✓||
|mint|✓|✓|✓||
|nixos|✓|✓|||
|opensuse|✓|✓|||
|pop_os|✓|✓|✓||
|rockylinux|✓|✓|||
|tails||||Tails images can only be booted from an ext4 partition|
|ubuntu|✓|✓|✓||
|zorin|✓|✓|✓||

## How does it work ?

The LinuxLoops bash script will create a disk image containing a 16MB EFI partition, a 1GB boot partition, the main rootfs partition and an optional partition for swap. Distros will be installed in the image and an initramfs hook will allow booting the disk image through a specific grub config.

The minimum size for a LinuxLoops image has been defined as 10GB (with at least 8GB for the main rootfs) as it should allow most distros to install without issue. However, if you intend to install gentoo you will most likely need 40 GB minimum for the main rootfs (as it needs a lot of disk space to build everything from source).

Some use cases for LinuxLoops:
- To keep Windows or ChromeOS as the main OS on the computer and intall Linux without modifying the partition table.
- To use separate linux environments for different purposes (work, gaming...) without having to deal with complex partition tables.
- To easily setup Linux distros with fully encrypted rootfs and swap (the EFI and boot partitions are not encrypted).
- To have a full Linux environment which can also be used as a VM from another OS.
- For easy backup management, backing up a distro is as simple as copying a file.
- You tell me...

**Warning: Keep in mind that even though they are stored in image files, LinuxLoops are full Linux distros with complete access to your hardware so don't do anything that you would not do in a standard Linux install. Moreover, the LinuxLoops init script has a few dependencies on Linux distros fundamentals (notably the kernel/initramfs naming convention and the presence of a few packages such as bash, cryptsetup and udev), a significant change on those basics should be very rare but might break your install. Even though, if something goes wrong you should always be able to recover your data by mounting the disk image from another LinuxLoops image or from a Linux live usb (see Data-recovery.md), make sure to keep regular backups of your data and keep in mind that this software is provided as is without any guarantee of any kind.**

<!-- Supported Hardware -->
## Supported Hardware

✔ Base Requirements:
- x86_64 based computer.
- Secure boot disabled.
- Administrative privileges on the device.
- 10 GB available space.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

## Encryption

The data in LinuxLoops images can be encrypted (rootfs and swap, leaving only the efi and boot partitions unencrypted).

Encryption is highly recommended as it protects physical access to your personal data, however it slightly impacts performance.
  
If you decide to setup encryption, you will receive an encryption password prompt early in the boot process while the keyboard is setup with a Qwerty layout, as such:
- Either Learn how to type your password as if your keyboard was Qwerty.
- Or choose a password which is identical when typed on a Qwerty keyboard.

## Install Instructions
This guide has been split into seperate sections, please follow one of the links below for a guide suitable to your current operating system.

### [Install with Linux][linux-guide]
### [Install with Windows][windows-guide]
### [Install with Brunch (singleboot)][brunch-guide]
### [Install with ChromeOS (RW_LEGACY firmware needed)][chromeos-guide]


## Complementary instructions
You will find below additional instructions aiming to improve your LinuxLoops experience.

### [Custom install parameters][custom-guide]
### [Use the image in a virtual machine][vm-guide]
### [Data recovery from an image][recovery-guide]

## Support

Support for LinuxLoops is currently provided in the LinuxLoops section of the brunch Discord:

[![Discord][discord-shield]][discord-url]

## Pull requests

Clearly, in its current state, LinuxLoops is not perfect and I am counting on the community to help by submitting pull requests. However, those needs to respect the ground project principles:
- LinuxLoops partitioning scheme is fixed, it has been defined to limit as much as possible dependencies and to ensure a good performance.
- Basic desktop environment targets should be debloated (the DE, a terminal and a file browser).
- Full desktop environment targets are not based on users preferences but on the choices of the distro managers.
- Lightdm is used by default for basic targets as it is lightweight and widely compatible (aside from gnome desktop targets which often depend on gdm).

If you need something else, read about custom scripts or feel free to make your own fork of LinuxLoops.

<!-- Special Thanks -->

## Special Thanks

First of all, thanks goes to:
- The [lxc/lxd][lxc link] project for maintaining Linux container rootfs archives.
- The [Linux-Surface crew][linux-surface link] for greatly improving Linux support on Surface devices.
- [MrChromebox][MrChromebox link] for its awesome Chromebooks custom firmwares.
- The [Chromebrew][Chromebrew link] framework which allows encryption support for brunch / chromeos.

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

<!-- Outbound Links -->
[lxc link]: https://linuxcontainers.org/
[linux-surface link]: https://github.com/linux-surface/linux-surface
[MrChromebox link]: https://mrchromebox.tech/
[Chromebrew link]: https://github.com/skycocker/chromebrew

<!-- Internal Links -->
[windows-guide]: ./Install-with-windows.md
[linux-guide]: ./Install-with-linux.md
[brunch-guide]: ./Install-with-brunch.md
[chromeos-guide]: ./Install-with-chromebook.md
[custom-guide]: ./Custom-install.md
[vm-guide]: ./Virtual-Machines.md
[recovery-guide]: ./Data-recovery.md
