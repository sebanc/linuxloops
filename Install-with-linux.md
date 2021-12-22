<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]

<!-- Installation Guides -->
This guide is for installing LinuxLoops on your computer from Linux. There are two variants, you can choose to install to boot LinuxLoops images directly from your HDD Linux distro grub or use an USB flashdrive as the LinuxLoops bootloader.

# Before you start

LinuxLoops can only boot from unencrypted ext4 partitions so make sure that the destination partition is in ext4 format.

# 1st method: Using your installed Linux distro grub as bootloader (Boot the image from HDD)

<details>
  <summary>Click to open the LinuxLoops GUI install guide with your installed Linux distro grub as bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- 10 GB available space on an unencrypted ext4 partition.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Make sure the curl, cryptsetup, fdisk, nano, tar and zenity packages/binaries are installed in your Linux distro.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Create a directory for linuxloops images where you want (in this example we will create a LinuxLoops directory within the user account path)

`mkdir ~/linuxloops`
  
4. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops-beta/main/linuxloops`
  
5. Launch the GUI installer:

`sudo bash linuxloops`

6. Follow the installer menu, choosing the distro, desktop environment, image path... (in this example the image path would be /home/username/linuxloops)

7. Create a copy of your existing 40_custom file.

`sudo cp /etc/grub.d/40_custom /etc/grub.d/99_linuxloops`

8. Open the 99_linuxloops file in an editor. For this guide we'll be using nano but you can use gedit, vi, or any editor of your choice.

`sudo nano /etc/grub.d/99_brunch`

9. Copy/Paste the Grub Boot Entries displayed in the installer in the file and press Ctrl + X, then Y to save and Enter to confirm.

10. After saving, commit the new entries to Grub.

`sudo grub-mkconfig -o /boot/grub/grub.cfg`

11. Reboot your computer and start the LinuxLoops grub entry from your distro's grub menu.

</details>

<details>
  <summary>Click to open the LinuxLoops command line install guide with your installed Linux distro grub as bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- 10 GB available space on an unencrypted ext4 partition.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Make sure the curl, cryptsetup, fdisk, nano, tar and zenity packages/binaries are installed in your Linux distro.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Create a directory for linuxloops images where you want (in this example we will create a LinuxLoops directory within the user account path)

`mkdir ~/linuxloops`
  
4. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops-beta/main/linuxloops`

5. List available distros and desktop environments:

`sudo bash linuxloops -l`

6. Launch the installer:

Arguments description:
"-dist <distribution>": selects the linux distro (mandatory)  
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is generally selected by default)  
"-img <path>": set the path to the disk image such as: ~/linuxloops/distro.img  
"-s" <number>: size of the disk image in GB (optional, 10GB by default)  
"-z" <number>: size of the swap (optional) (optional, no swap by default)  
"-e": enable rootfs and swap partitions encryption (optional but highly recommended)  
"-S": automatically applied Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default)  

`sudo bash linuxloops -dist ubuntu -env kde-full -img ~/linuxloops/ubuntu.img -s 24 -z 4 -e`

7. Create a copy of your existing 40_custom file.

`sudo cp /etc/grub.d/40_custom /etc/grub.d/99_linuxloops`

8. Open the 99_linuxloops file in an editor. For this guide we'll be using nano but you can use gedit, vi, or any editor of your choice.

`sudo nano /etc/grub.d/99_brunch`

9. Copy/Paste the Grub Boot Entries displayed in the installer in the file and press Ctrl + X, then Y to save and Enter to confirm.

10. After saving, commit the new entries to Grub.

`sudo grub-mkconfig -o /boot/grub/grub.cfg`

11. Reboot your computer and start the LinuxLoops grub entry from your distro's grub menu.

</details>

# 2nd method: Use an USB flashdrive as bootloader (Boot the image from USB)

<details>
  <summary>Click to open the LinuxLoops GUI install guide with an USB flashdrive as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- Windows 11 with Ubuntu WSL2 installed.
- 10 GB available space on an unencrypted ext4 partition.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Make sure the curl, cryptsetup, fdisk, nano, tar and zenity packages/binaries are installed in your Linux distro.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Create a directory for linuxloops images where you want (in this example we will create a LinuxLoops directory within the user account path)

`mkdir ~/linuxloops`
  
4. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops-beta/main/linuxloops`

5. Download the USB bootloader template image.

`curl -O -L https://github.com/sebanc/linuxloops-beta/raw/main/usb_bootloader.img`
  
6. Launch the GUI installer:

`sudo bash linuxloops`

7. Follow the installer menu, choosing the distro, desktop environment, image path... (in this example the image path would be /home/username/linuxloops)

8. Use 'dd' to write usb_bootloader.img file from your Downloads folder to a USB flashdrive.

`sudo dd if=usb_bootloader.img of=/dev/<your_usb_flashdrive>`

9. Reboot your computer and select your USB flashdrive as boot device in the BIOS.

</details>

<details>
  <summary>Click to open the LinuxLoops command line install guide with an USB flashdrive as a bootloader</summary>

### Requirements
- Administrator access.
- Secure boot disabled.
- 10 GB available space on an unencrypted ext4 partition.
- An entry level understanding of the linux terminal.
  - This guide aims to make this process as easy as possible, but knowing the basics is expected.

### Installation steps

1. Make sure the curl, cryptsetup, fdisk, nano, tar and zenity packages/binaries are installed in your Linux distro.

2. Change the directory to your Downloads folder.

`cd ~/Downloads`

3. Create a directory for linuxloops images where you want (in this example we will create a LinuxLoops directory within the user account path)

`mkdir ~/linuxloops`

4. Download the linuxloops script:

`curl -O -L https://raw.githubusercontent.com/sebanc/linuxloops-beta/main/linuxloops`

5. Download the USB bootloader template image.

`curl -O -L https://github.com/sebanc/linuxloops-beta/raw/main/usb_bootloader.img`
  
6. List available distros and desktop environments:

`sudo bash linuxloops -l`

7. Launch the installer:

Arguments description:
"-dist <distribution>": selects the linux distro (mandatory)
"-env <desktop_environment>": selects the default desktop environment (optional, gnome desktop environment is generally selected by default)
"-img <path>": set the path to the disk image such as: ~/linuxloops/distro.img
"-s" <number>: size of the disk image in GB (optional, 10GB by default)
"-z" <number>: size of the swap (optional) (optional, no swap by default)
"-e": enable rootfs and swap partitions encryption (optional but highly recommended)
"-S": automatically applied Microsoft Surface patches from www.github.com/linux-surface (optional, Surface patches are not included by default)

`sudo bash linuxloops -dist ubuntu -env kde-full -img ~/linuxloops/ubuntu.img -s 24 -z 4 -e`

8. Use 'dd' to write usb_bootloader.img file from your Downloads folder to a USB flashdrive.

`sudo dd if=usb_bootloader.img of=/dev/<your_usb_flashdrive>`

9. Reboot your computer and select your USB flashdrive as boot device in the BIOS.

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

