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

2. Download the Linuxloops script:  

`curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -O --create-dirs --output-dir ~/bin`  
  
3. Launch the Linuxloops script  

- To use the GUI installer, install the `PyQtWebEngine` package:  
`sudo apt install python3-venv python3-pyqt6.qtwebengine`  

- To use the CLI installer:  
```
Usage: sudo bash ~/bin/linuxloops -distro <distribution name> -env <environment name> -dst <disk name or disk image path>
-distro, --distribution <distribution name>		(Distribution to install)
-env, --environment <environment name>			(Environment to install)
-dst, --destination <disk name or disk image path>	(e.g. /dev/sda or /ubuntu.img)
-s, --size <total install size>				(number in GB, minimum 14GB)
-z, --swapsize <swap size>				(number in GB)
-b, --btrfs						(Use btrfs for the root filesystem)
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
-d, --declarative <config_file_path>			(Use a declarative configuration file)
-m, --custom-mirror <mirror details>			(Add a custom mirror according to the below format:
							<repository>*<mirror>
							ex: Arch*https://mirrors.kernel.org/archlinux)
-p, --user-password-for-encryption			(Use user account password for encryption)
-l, --list						(List available distributions and environments)
-ll, --list-locales					(List available locales)
-lk, --list-keymaps					(List available keymaps)
-lt, --list-timezones					(List available timezones)
-h, --help						(Display this menu)
```

The only mandatory parameters are: the distribution, the environment and the destination. Use the below command to list available distributions and environments:  
`sudo bash ~/bin/linuxloops -l`  

As an example:  
`sudo bash ~/bin/linuxloops -distro Arch -env Cinnamon -dst /mnt/c/Users/"username"/Downloads/Arch.img -s 14` will install Arch with the cinnamon desktop environment in a 14 GB image located at C:\Users\"username"\Downloads\Arch.img.  

- To use the Declarative installer:  

Have a look at the declarative configuration examples available here:  
[Declarative configuration examples][Declarative configuration examples]  

The only mandatory parameters are: the distribution, the environment and the destination. Use the below command to list available distributions and environments:  
`sudo bash ~/bin/linuxloops -l`  

Create your own declarative configuration and run the below command to start the install:  
`sudo bash ~/bin/linuxloops -d <path_to_your_declarative_configuration>`  

4. Finalisation (For disk installs)  

Use a software like Rufus or Etcher to write the image located at C:\Users\"username"\Downloads\Arch.img on a drive.  

Once install is complete, reboot your computer and choose your drive in the UEFI BIOS boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Arch.der, confirm and reboot your computer.  

4. Finalisation (For disk image installs)  

Install and open Grub2Win, click on "Manage Boot Menu" -> "Add a new entry" -> set "Type" as "Create user section", open the file C:\Users\"username"\Downloads\Arch.img.grub.txt and copy its content in the Grub2Win notepad window, save and close the Grub2Win notepad window then click "Apply" and "OK".  

Start the Linuxloops grub entry from your Grub2Win menu.  

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
