<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guides -->
This guide is for installing LinuxLoops on your computer from a Chromebook. This method requires a custom firmware (RW_LEGACY or ALT FW depending on your chromebook, refer to MrChromebox website for more information) with HDD boot as default.

<details>
  <summary>Click to open the LinuxLoops command line install guide with MrChromebox custom firmware</summary>

### Requirements
- Developer mode.
- MrChromebox custom firmware (RW_LEGACY or ALT FW depending on your chromebook, refer to MrChromebox website for more information)
- 10 GB available space.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Install MrChromebox custom firmware (RW_LEGACY or ALT FW depending on your chromebook, refer to MrChromebox website for more information) with HDD boot as default.

2. (Optional) If you want to the linuxloops image to be encrypted (highly recommended) install Chromebrew and the "cryptsetup" Chromebrew package (refer to Chromebrew online resources).

3. Change the directory to your Downloads folder.

`cd ~/Downloads`

4. Create a directory for linuxloops images on the unencrypted part of the data partition:

`sudo mkdir /mnt/stateful_partition/unencrypted/linuxloops`
  
5. Install the linuxloops script:

```
sudo chown 1000:1000 /usr/local
mkdir -p /usr/local/bin
curl -L https://raw.githubusercontent.com/sebanc/linuxloops/main/linuxloops -o /usr/local/bin/linuxloops
chmod 0755 /usr/local/bin/linuxloops
```

6. List available distros and desktop environments:

`sudo bash linuxloops -l`

7. Launch the installer:

Arguments description:
"-dist <distribution>": selects the linux distro (mandatory)
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is generally selected by default)
"-img <path>": set the path to the disk image such as: /mnt/stateful_partition/unencrypted/linuxloops/distro.img
"-s" <number>: size of the disk image in GB (optional, 10GB by default)
"-z" <number>: size of the swap (optional) (optional, no swap by default)
"-e": enable rootfs and swap partitions encryption (optional but highly recommended)
"-S": automatically applied Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default)

`sudo bash linuxloops -dist ubuntu -env kde-full -img /mnt/stateful_partition/unencrypted/linuxloops/ubuntu.img -s 24 -z 4 -e`

8. Reboot your Chromebook and press CTRL+L on the developer mode screen to boot the linuxloops image.

</details>

### What to do after installation
- Get familiar with the package manager of the distro you have installed (refer to the chosen distro's online resources)
- Set-up your language and timezone (refer to the chosen distro's online resources)
- Create additional users if needed.
- Install your favorite software and enjoy.

In case you run into issues while installing or using LinuxLoops, you can find support in the LinuxLoops section of the brunch discord group:

[![Discord][discord-shield]][discord-url]

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops-beta?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops-beta?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops-beta/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M

