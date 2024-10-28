<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# LinuxLoops live image

A Linuxloops live image is available in the releases section of this github repository.  

This live image contains a Debian system with Linuxloops installed by default to make the installation process even easier.  
You can also install disk images grub boot configurations to the Linuxloops live image.  

The default password for the "live" user account is: "linuxloops".  

✔ Base Requirements:  
- x86_64 based computer with UEFI BIOS.  
- Administrative privileges on the device.  
- A 16GB (or more) USB flashdrive.  


## With Linux

Download the live image and run the following command to write it to the disk (this example assumes your drive is /dev/sdX:  

`7z x linuxloops_live_XXXXXXXX.7z linuxloops_live_*.img -so | sudo dd iflag=fullblock of=/dev/sdX oflag=direct conv=fsync bs=1M status=progress`  

Reboot your computer and select the USB flashdrive from the UEFI boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Debian.der, confirm and reboot your computer.  

## With Windows

Install 7zip and extract the linuxloops_live_XXXXXXXX.7z file.  

Write the resulting image file to your USB flashdrive using Rufus, Etcher or a similar tool.  

Reboot your computer and select the USB flashdrive from the UEFI boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Debian.der, confirm and reboot your computer.  


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

