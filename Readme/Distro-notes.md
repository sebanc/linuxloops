<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Distributions specific notes

## AlmaLinux

On the first boot after install, almalinux will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and almalinux should boot normally on the second boot.  

### Specific note for almalinux installation in a disk image with secure boot enabled

Disk images use the actual almalinux secure boot key. When the almalinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:  
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## Arch

archlinux does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.  


## Artix

artixlinux does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.  


## Brunch

Before installing brunch, please refer to the [brunch readme][brunch-readme] for more information on device compatibility.  
Please raise brunch issues on the brunch github repository.  


## ChromeOS-Flex

The full-devmode target allows to enable developer mode by default.  


## Fedora

On the first boot after install, fedora will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and fedora should boot normally on the second boot.  

If you install the nvidia proprietary driver, the first boot after each kernel update will be long as the nvidia kernel modules are being rebuilt.  


## Gentoo

If you intend to install gentoo with a desktop environment, you will most likely need 40 GB minimum for the main rootfs (as it needs a lot of disk space to build everything from source).  

### Specific note for gentoo installation on disk with secure boot enabled

gentoo does not have secure boot support out of the box. Nevertheless, secureboot can be enabled manually by emerging `mokutil` and running the below commands:  
```
sudo mv /boot/efi/EFI/BOOT/BOOTX64.EFI /boot/efi/EFI/BOOT/grubx64.efi
sudo cp /usr/share/shim/BOOTX64.EFI /boot/efi/EFI/BOOT/BOOTx64.EFI
sudo cp /usr/share/shim/mmx64.efi /boot/efi/EFI/BOOT/
sudo sbsign --key /etc/secureboot_key/MOK.key --cert /etc/secureboot_key/MOK.crt --output /boot/efi/EFI/BOOT/grubx64.efi /boot/efi/EFI/BOOT/grubx64.efi
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## Kali

Kali does not have secure boot support in full disk install.  


## Manjaro

manjaro does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.  


## NixOS

After install, if you want to install packages via nix, open the teminal and run "sudo nix-channel --update" first.  


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


## RockyLinux

On the first boot after install, rockylinux will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and fedora should boot normally on the second boot.  

### Specific note for rockylinux installation in a disk image with secure boot enabled

Disk images use the actual rockylinux secure boot key. When the rockylinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:  
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.  


## SteamOS

SteamOS installed from the 3.5 branch of the SteamOS packages repository (https://steamdeck-packages.steamos.cloud/archlinux-mirror/) with minor adjustments to support standard computers usage.  
SteamOS packages can be installed and updated with pacman, however native packages available in SteamOS are not the latest versions, therefore for sensitive apps such as web browsers and such it is recommended to use the flatpak version (available by default in the Discover app).  

3 environments are available:
- desktop: Boots to SDDM in order to support multi-users setup. The gamescope session can be launched within Plasma through the "SteamDeck Session" shortcut (in "Game" section).  
- desktop-autologin: Auto-login into Plasma. The gamescope session can be launched within Plasma through the "SteamDeck Session" shortcut (in "Game" section).  
- gamescope-session: Same as the SteamDeck. Boots directly into the SteamOS session. Plasma can be launched with the "Switch to Desktop" SteamOS option.  

Note: Due to a bug with xdg-desktop-portal-kde that has not yet been corrected in the SteamOS repositories, flatpak apps will trigger an "app running in the background" plasma notification. Either disable those types of notifications entirely in plasma settings or install flatseal and allow "run in the background" permission for each app.  


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

