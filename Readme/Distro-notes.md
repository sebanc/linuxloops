<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Distributions specific notes

### Specific note for almalinux installation in a disk image with secure boot enabled

Disk images use the actual almalinux secure boot key. When the almalinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:  
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## Arch

Arch Linux does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## Artix

Artix Linux does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## Bazzite

Secure boot does not work out of the box on Bazzite, you have to disable secure boot in the bios first, then boot into Bazzite and run:  
`sudo mokutil --import /etc/secureboot_key/MOK.der`  
Reboot, enroll the key in shim and re-enable secureboot.  


## BlendOS

BlendOS does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## Brunch

Before installing brunch, please refer to the [brunch readme][brunch-readme] for more information on device compatibility.  
Please raise brunch issues on the brunch github repository.  


## CachyOS

CachyOS does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## ChromeOS-Flex

Devmode is only available when installing ChromeOS-Flex in a disk image.  
Disk images cannot be booted from a btrfs partition due to the absence of btrfs support in the ChromeOS-Flex kernel config.  


## Fedora

If you install the nvidia proprietary driver, the first boot after each kernel update will be long as the nvidia kernel modules are being rebuilt.  


## Fedora-Atomic

If you install the nvidia proprietary driver, you will need to disable Secure Boot.  


## FoxFlake

FoxFlake proposes 3 bundles of apps that respectively contain:  
- Standard bundle: Firefox, Thunderbird and LibreOffice.  
- Gaming bundle: Steam, Heroic and Lutris.  
- Studio bundle: DaVinci Resolve, OBS Studio, Blender, Kdenlive, GIMP, Audacity.  

For more information on FoxFlake, please refer to the [FoxFlake readme][foxflake-readme].  


## Kali

Kali does not have secure boot support in full disk install.  


## KDE

KDE Linux installed as a rolling release distro.  
KDE Linux is based on Arch that does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## Manjaro

Manjaro does not have secure boot support through its official repository. Linuxloops will install the "shim-signed" bootloader AUR package.  


## OpenSUSE

### Specific note for OpenSUSE installation in a disk image with secure boot enabled

Disk images use the actual OpenSUSE secure boot key. When the OpenSUSE secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:  
```
sudo cp /usr/share/efi/x86_64/grub.der /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## Parrot

parrot does not have secure boot support in full disk install.  


## Qubes

On the first boot you will be prompted to configure qubes, if you experience a crash after the first boot with the default qubes settings you should disable usb qubes in the configuration menu.  


### Specific note for rockylinux installation in a disk image with secure boot enabled

Disk images use the actual rockylinux secure boot key. When the rockylinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:  
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## SteamOS

SteamOS installed from the SteamOS packages repository (https://steamdeck-packages.steamos.cloud/archlinux-mirror/) with minor adjustments to support standard computers usage.  
Packages can be installed and updated with pacman, however native packages available in the SteamOS packages repository are not the latest versions, therefore for sensitive apps such as web browsers and such it is recommended to use the flatpak version (available by default in the Discover app).  

2 environments are available:
- Desktop: Boots to Plasma session. The gamescope session can be launched within Plasma through the "SteamDeck Session" shortcut (in "Game" section).  
- Gamescope: Same as the SteamDeck. Boots directly into the SteamOS session. Plasma can be launched with the "Switch to Desktop" SteamOS option.  

Note: The gamescope session is not compatible with nvidia gpu but you can use the standard steam app within a desktop environment.  


## Tails

Tails disk images can only be installed on ext4 partitions (due to the lack of kernel modules for ntfs / exfat support in its initramfs).  


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

<!-- Internal Links -->
[brunch-readme]: https://github.com/sebanc/brunch/blob/main/README.md
[foxflake-readme]: https://github.com/sebanc/foxflake/blob/main/Readme.md

