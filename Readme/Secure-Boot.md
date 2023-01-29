<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Secure Boot support
  
  ***

SecureBoot is not always supported by Linux distributions and most distributions supporting it rely on the Shim bootloader. Linuxloops secure boot implementation is therefore also based on the Shim bootloader, nevertheless you can manually switch to your preferred method if needed (replacement of platform key...).

In case you only want to enable secureboot for specific Windows 11 / games support but you are not actually interested by the security benefits it brings, you may want to consider disabling the validation process in shim by running `mokutil --disable-validation` which will allow you to boot any kernel/bootloader without actually disabling secureboot.

## Secure boot support for full disk installs

If the chosen distro supports SecureBoot natively (notably the case for gentoo, kali, nixos, parrot), secureboot will be supported by default.

Otherwise, during install, the Linuxloops script generates a basic secure boot key (which is used both for kernel and dkms modules signing) in /etc/secureboot_key directory and copies the secure boot DER Machine Owner Key certificate in the EFI partition.

On the first boot, a blue screen saying "Verification failed: Access Denied" will appear and you will have to enroll the secure boot key by selecting "OK->Enroll key from disk->EFI->MOK.der->Continue".

Reboot your device and the linux distro will start normally.

## Secure boot support for disk images installs

Requirement: Installed linux distro with secureboot enabled through Shim.

In the case of disk images, SecureBoot support will rely on your main linux distribution shim bootloader.

During install, the Linuxloops script generates a basic secure boot key (which is used both for kernel and dkms modules signing) in /etc/secureboot_key directory and copies the secure boot DER Machine Owner Key certificate in the disk image folder as "<image_name>.img.der".

After creating the image, run `sudo mokutil --import <image_path>/<image_name>.img.der`
 
Reboot your device and launch the image specific grub entry.

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
