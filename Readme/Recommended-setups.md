<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Recommended setups

Those recommended setups aim at avoiding unnecessarily complex partition tables when several OS images are installed.  


## My main OS is Linux and I don't use windows

Evaluate the space you will want to give to your Linuxloops OS images and add an unencrypted ext4 or btrfs partition to store your Linuxloops disk images.  


## My main OS is Linux and I occasionaly use Windows (Installing windows in a disk image)

Same principle as above but leave some unallocated space for your windows installation (Windows 11 requires at least 64 GB if you want to be able to update it).  

Boot a Windows 11 installation USB flash drive on your computer.  

Move on until you reach "Where do you want to install Windows ?" screen.  

Format the unallocated space as "NTFS".  

press Shift + F10 keys to open a command prompt.  

Type `diskpart` into the command prompt.  

use "list volume" and identify the drive letter of the newly created partition for the windows image.  

Type `create vdisk file="<drive letter>:\<file name>.vhdx" maximum=<size in MB> type=fixed`  

Then run `attach vdisk` and then `exit` to exit diskpart.  

Close the command prompt.  

Select the newly created virtual disk in the list and continue windows setup.  

Once Windows is installed, go to your UEFI BIOS settings and set your efi boot priority back to your main linux install.  

If not already the case, enable grub osprober in your linux distribution in order to be able to boot windows from grub.  


## My main OS is Windows and I occasionality need a linux distribution

Requirement: Secure Boot disabled.  

Evaluate the space you will want to give to your Linuxloops OS images, Open Windows Disk Management, free up disk space and create an ExFAT partition.  

Install Grub2Win.  

Install your disk images on the ExFAT partition and copy the Linuxloops grub configurations in Grub2Win.  

Reboot and launch your Linuxloops images from Grub2Win.  


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

