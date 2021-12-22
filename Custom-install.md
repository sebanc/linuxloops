<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Custom installs
  
  ***
<!-- This *** line creates a divider so that the dropdown looks nice. 
Empty lines between everything in <angle breackets> is intentional due to markdown issues -->

In some cases, you might want to include some packages during the LinuxLoops installation process, this is mainly useful if you do not have wifi out of the box after a standard Linux install.

## The needed package is available in the main linux distro repository

1. Identify the needed package name by browsing the linux distro repositories / forums.

2. When you run the linuxloops script, add the needed package in the CUSTOM_PACKAGES variable. For example, if the needed package is "broadcom-sta-dkms", run

`CUSTOM_PACKAGES="broadcom-sta-dkms" sudo bash linuxloops ....`

## The needed package is not available in a different repository, on github ...

In that case you will need to create a custom script.

1. Create a file named "custom_script" in the directory from which you are going to run the linuxloops script (the directory in the terminal when you run the script, usually your Downloads folder)

2. Add in this file all the commands needed to install your driver, for example:
```
cd /tmp
git clone https://github.com/aircrack-ng/rtl8814au.git
cd rtl8814au
make
make install
```

This script will be run at the end of the installation process as "root" so make sure the commands are run from /tmp (keep the first line of this example "cd /tmp") and do not use sudo.

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/brunch?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/brunch?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/brunch/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
