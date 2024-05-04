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

`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -o ~/linuxloops`  
  
2. Launch the Linuxloops script  

- To use the GUI installer, install the `zenity` package for your distro and then run:  

`sudo bash ~/linuxloops`

- To use the CLI installer:  
```
Usage: sudo bash linuxloops -distro <distribution name> -env <desktop environment> -dst <disk name or disk image path> [-s <total install size>] [-z <swap size>] [-b] [-e] [-a] [-H <hostname>] [-L <locale>] [-K <keymap>] [-T <timezone>] [-n] [-S] [-c <custom_packages_list>] [-C <custom_script_path>] [-k <kernel_parameters_list>]
-distro, --distribution <distribution name>			(Distribution to install)
-env, --environment <desktop environment>			(Desktop environment to install)
-dst, --destination <disk name or disk image path>		(e.g. /dev/sda or /ubuntu.img)
-s, --size <total install size>					(number in GB, minimum 14GB)
-z, --swapsize <swap size>					(number in GB)
-b, --btrfs							(Use btrfs for the root filesystem)
-e, --encrypt							(Encrypt the root filesystem)
-a, --autologin							(Enable user autologin)
-H, --hostname							(Provide a specific hostname)
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
`sudo bash ~/linuxloops -distro Arch -env Cinnamon -dst ~/arch.img -s 30 -S` will install Arch with the cinnamon desktop environment and linux-surface patches in a 30 GB image located at /home/username/arch.img.  

- To use the Declarative installer:  

Have a look at the declarative configuration examples available here:  
[Declarative configuration examples][Declarative configuration examples]  

The only mandatory parameters are: the distribution, the environment and the destination. Use the below command to list available distributions and environments:  
`sudo bash ~/linuxloops -l`  

Create your own declarative configuration and run the below command to start the install:  
`sudo bash ~/linuxloops -d <path_to_your_declarative_configuration>`  

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

Start the Linuxloops grub entry from your distro's grub menu.  

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
