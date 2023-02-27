<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Distributions specific notes
  
  ***


## almalinux

On the first boot after install, almalinux will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and almalinux should boot normally on the second boot.

### Specific note for almalinux installation in a disk image with secure boot enabled

Disk images use the actual almalinux secure boot key. When the almalinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.


## archlinux

archlinux does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.


## artixlinux

artixlinux does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.


## brunch

Before installing brunch, please refer to the [brunch readme][brunch-readme] for more information on device compatibility.
Please raise brunch issues on the brunch github repository.


## chromeos-flex

The full-devmode target allows to enable developer mode by default.


## fedora

On the first boot after install, fedora will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and fedora should boot normally on the second boot.

If you install the nvidia proprietary driver, the first boot after each kernel update will be long as the nvidia kernel modules are being rebuilt.


## gentoo

If you intend to install gentoo with a desktop environment, you will most likely need 40 GB minimum for the main rootfs (as it needs a lot of disk space to build everything from source).

### Specific note for gentoo installation on disk with secure boot enabled

gentoo does not have secure boot support OOTB. Nevertheless, secureboot can be enabled manually by emerging `mokutil` and running the below commands:
```
sudo mv /boot/efi/EFI/BOOT/BOOTX64.EFI /boot/efi/EFI/BOOT/grubx64.efi
sudo cp /usr/share/shim/BOOTX64.EFI /boot/efi/EFI/BOOT/BOOTx64.EFI
sudo cp /usr/share/shim/mmx64.efi /boot/efi/EFI/BOOT/
sudo sbsign --key /etc/secureboot_key/MOK.key --cert /etc/secureboot_key/MOK.crt --output /boot/efi/EFI/BOOT/grubx64.efi /boot/efi/EFI/BOOT/grubx64.efi
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.


## kali

Kali does not have secure boot support in full disk install.


## manjaro

manjaro does not have secure boot support through its official repository. Linuxloops will pre-install the "shim-signed" bootloader AUR package.


## nixos

After install, if you want to install packages via nix, open the teminal and run "sudo nix-channel --update" first.


## opensuse

### Specific note for opensuse installation in a disk image with secure boot enabled

Disk images use the actual opensuse secure boot key. When the opensuse secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:
```
sudo cp /usr/share/efi/x86_64/grub.der /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.


## parrot

parrot does not have secure boot support in full disk install.


## rockylinux

On the first boot after install, rockylinux will relabel files for Selinux support (this might take a few minutes) and reboot. This is the expected behaviour and fedora should boot normally on the second boot.

### Specific note for rockylinux installation in a disk image with secure boot enabled

Disk images use the actual rockylinux secure boot key. When the rockylinux secure boot key changes which should be very rare, you will need to disable secure boot temporarily and enroll the new key with mokutil by running:
```
sudo cp /usr/share/pki/sb-certs/secureboot-kernel-x86_64.cer /etc/secureboot_key/MOK.der
sudo mokutil --import /etc/secureboot_keys/MOK.der
```
Reboot, enroll the key in shim and re-enable secureboot.


## steamos-like

steamos-like is not a real distro, it is just a 100% standard archlinux with a few specific configuration files (no binaries) allowing to launch a SteamOS Gamescope session. However, as it is intended for PC, it has been set to boot by default in Plasma for standard use and will allow you to launch a Gamescope session through a desktop shortcut.

By design, this implementation of the gamescope session has some limitations similar to the ones on the Steamdeck: you can only have 1 user and auto-login through SDDM is mandatory.
Nevertheless, as long as the above requirements are satisfied, it is 100% archlinux so you can install any native arch package and update them through pacman, the discover app...

On the first boot:
- If you use wifi, connect to your wifi network through plasma network-manager, then go to plasma network settings and make the wifi connection "Available to all users".
- Login your steam account.
- Launch the gamescope session.

Currently, aside from AMD GPU which are generally well supported, the SteamOS session is not fully stable on all GPU (due to different gamescope / mesa / steam issues). The following should help fixing issues with Intel and Nvidia GPUs.
- Opt-in the beta of the steam client (the option is in the first page in the application settings).
- Build the below specific branch of mesa:
```
git clone https://aur.archlinux.org/mesa-git.git
cd mesa-git/
sed -i 's@https://gitlab.freedesktop.org/mesa/mesa.git#branch=main@https://gitlab.freedesktop.org/GL/mesa.git#branch=usage_checks_fixes@g' PKGBUILD
makepkg -si
```


## tails

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
