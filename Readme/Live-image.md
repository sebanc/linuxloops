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

Download the linuxloops live 7z archive in the release section of this Github repository and either:  

- Extract it using your archive manager (you might need to first install the `7zip` package) and write it to a USB flashdrive using an image writer (Gnome Disk Utility / KDE ISO Image Writer).  

- Or use the below terminal command from the directory containing the linuxloops live image 7z archive to write it to a disk (this example assumes your USB flashdrive is /dev/sdX:  

`7z x $(ls linuxloops_live_????????.7z | tail -1) linuxloops_live_*.img -so | sudo dd iflag=fullblock of=/dev/sdX oflag=direct conv=fsync bs=1M status=progress`  

Reboot your computer and select the USB flashdrive from the UEFI boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Debian.der, confirm and reboot your computer.  

Once the live image has booted, set your keyboard layout (Preferences -> Keyboard -> Layout), connect to WiFi if needed and launch the "Linuxloops installer" from the desktop icon.  

## With Windows

Install 7zip, download the linuxloops live 7z archive in the release section of this Github repository and extract the linuxloops live 7z archive.  

Write the resulting image file to your USB flashdrive using balenaEtcher.  

Reboot your computer and select the USB flashdrive from the UEFI boot menu.  

If Secure Boot is enabled, you should see the blue shim screen, select "Enroll key from disk" -> EFI -> Debian.der, confirm and reboot your computer.  

Once the live image has booted, set your keyboard layout (Preferences -> Keyboard -> Layout), connect to WiFi if needed and launch the "Linuxloops installer" from the desktop icon.  


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

