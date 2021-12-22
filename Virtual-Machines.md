<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Running LinuxLoops images in Virtual Machines
  
  ***
<!-- This *** line creates a divider so that the dropdown looks nice. 
Empty lines between everything in <angle breackets> is intentional due to markdown issues -->

LinuxLoops images can be run in Virtual Machines by treating them as raw disks. This section of the guide only covers VirtualBox for now and has to be completed for other virtualisation softwares.

**WARNING: Do not launch the currently running LinuxLoops image in a Virtual Machine. I don't see why anyone would want to do that but it will most likely break the image.**

## Using LinuxLoops disk images in VirtualBox

1. From the OS with VirtualBox installed, cd into the linuxloops image folder.

2. Create a virtual disk template for the linuxloops image:

From Windows: `C:\"Program Files"\Oracle\VirtualBox\VboxManage.exe internalcommands createrawvmdk -filename ubuntu.vmdk -rawdisk ubuntu.img`

From Linux: `VboxManage internalcommands createrawvmdk -filename ubuntu.vmdk -rawdisk ubuntu.img`

3. Open VirtualBox and setup a new virtual machine. When requested for the storage, select the vmdk file we have just created in the linuxloops image folder.

4. Open the VM settings -> System -> enable EFI

5. Start the VM

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops-beta?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops-beta?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops-beta/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
