<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# LinuxLoops live image
  
  ***

A linuxLoops live image is available in the releases section of github.

This live image contains a full system with linuxloops installed by default to make the installation process even easier.
Note: you can use install the grub configuration on a linuxloops live USB to boot images installed on your hdd.


## With Linux

Download the live image and run the following command to write it to the disk (this example assumes your drive is /dev/sdX:

`7z x linuxloops_live_XXXXXXXX.7z linuxloops_live_*.img -so | sudo tee /dev/sdX`


## With Windows

Install 7zip and extract the linuxloops_live_XXXXXXXX.7z file.

Write the resulting image file to your USB flashdrive using Rufus, Etcher or a similar tool.


<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

