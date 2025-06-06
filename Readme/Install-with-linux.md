<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guide -->
# Installation from Linux

## Requirements
- x86_64 based computer with UEFI BIOS.  
- Administrator access.  
- A drive with at least 14 GB available space.  

## Install guide

1. Download the Linuxloops script:  

`curl -L https://github.com/sebanc/linuxloops/raw/refs/heads/main/linuxloops -O --create-dirs --output-dir ~/bin`  
  
2. Launch the Linuxloops script  

- To use the GUI installer, install the below packages depending on your distribution:  
  * Debian / Ubuntu based distributions: `sudo apt install curl xz-utils python3-venv python3-gi gir1.2-gtk-3.0 gir1.2-webkit2-4.1`  
  * Arch based distributions: `sudo pacman -Syu --needed curl gnupg xz python-gobject gtk3 webkit2gtk-4.1`  
  * RHEL based distributions: `sudo dnf install curl gnupg xz python3-gobject gtk3 webkit2gtk4.1`  
  * OpenSUSE: `sudo zypper in  curl gnupg xz python3-gobject gtk3 typelib-1_0-WebKit2-4_1`  
  * Void: `sudo xbps-install -Syu curl xz python3-gobject gtk+3 webkit2gtk`  
  * Gentoo: `sudo emerge app-arch/xz-utils net-misc/curl dev-lang/python net-libs/webkit-gtk:4.1`  
  * NixOS: No packages to install (the necessary packages will be installed by linuxloops for use in nix-shell environment)  

Start linuxloops in GUI mode:  
`bash ${HOME}/bin/linuxloops`  

- To use the CLI installer:  

Make sure that `curl` and `xz` programs are installed.  

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

- To use the Declarative installer:  

Have a look at the declarative configuration examples available here:  
[Declarative configuration examples][Declarative configuration examples]  

The main parameters are: the distribution, the version and the environment. Use the below command to list available distributions and environments:  
`bash ${HOME}/bin/linuxloops -l`  

Create your own declarative configuration and run the below command to start the install:  
`bash ${HOME}/bin/linuxloops -d <path_to_your_declarative_configuration>`  

3. Finalisation (For disk installs)  

Once install is complete, reboot your computer and choose your drive in the UEFI BIOS boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Ubuntu.der, confirm and reboot your computer.  

3. Finalisation (For disk image installs)  

Create a the grub configuration needed to boot the image (according to the previous example):  

`cat /etc/grub.d/40_custom ~/arch.img.grub.txt | sudo tee /etc/grub.d/99_linuxloops`  

Commit the new entries to Grub.  

`sudo grub-mkconfig -o /boot/grub/grub.cfg`  

If Secure Boot is enabled, enroll the Secure Boot DER certificate:  

`sudo mokutil --import ~/arch.img.der`  

Choose a password, reboot your computer, you should see a blue screen, select "Enroll MOK" and validate with your chosen password.  

Start the Linuxloops grub entry from your Linux distribution's grub menu.  

## Support

Support for Linuxloops is provided in the dedicated section of the Brunch Discord server:  

[![Discord][discord-shield]][discord-url]

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

[Declarative configuration examples]: ../Declarative_configuration_examples
