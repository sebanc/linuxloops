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
- At least 14 GB available space.  

## Install guide

1. Launch WSL  

2. Download the linuxloops script:  

`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -o ~/linuxloops`  
  
3. Launch the Linuxloops script  

- To use the GUI installer, install the `zenity` package for your distro and then run:  

`sudo bash ~/linuxloops`

- Otherwise using the command line:  
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
`sudo bash ~/linuxloops -distro Arch -env Cinnamon -dst /mnt/c/Users/"username"/Downloads/Arch.img -s 14` will install Arch with the cinnamon desktop environment in a 14 GB image located at C:\Users\"username"\Downloads\Arch.img.  

4. Finalisation (For disk installs)  

Use a software like Rufus or Etcher to write the image located at C:\Users\"username"\Downloads\Arch.img on a drive.  

Once install is complete, reboot your computer and choose your drive in the UEFI BIOS boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Arch.der, confirm and reboot your computer.  

4. Finalisation (For disk image installs)  

Install and open Grub2Win, click on "Manage Boot Menu" -> "Add a new entry" -> set "Type" as "Create user section", open the file C:\Users\"username"\Downloads\Arch.img.grub.txt and copy its content in the Grub2Win notepad window, save and close the Grub2Win notepad window then click "Apply" and "OK".  

Start the LinuxLoops grub entry from your Grub2Win menu.  

## Support

Support for LinuxLoops is provided in the "LINUXLOOPS" section of the Brunch Discord server:  

[![Discord][discord-shield]][discord-url]

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

