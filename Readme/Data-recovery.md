<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Data recovery from an image
  
  ***

If something goes wrong (or for some other reason), you might want to recover data from a linux loop image while booting from another Linux install, a LinuxLoops image or from a Linux live usb.

<details>
  <summary>Recover data from an unencrypted linuxloops image</summary>

1. Run the following commands to mount the linuxloops rootfs:
```
mkdir -p ./chroot
image=$(losetup -fP --show <path_to_the_linuxloops_image>)
mount "$image"p3 ./chroot
```

2. Recover your data from the ./chroot folder

3. Unmount the linuxloops rootfs:

```
umount ./chroot
losetup -d "$image"
```

</details>

<details>
  <summary>Recover data from an encrypted linuxloops image</summary>

1. Run the following commands to mount the linuxloops rootfs:
```
mkdir -p ./chroot
image=$(losetup -fP --show <path_to_the_linuxloops_image>)
echo -n "<your_encryption_password>" | cryptsetup luksOpen "$image"p3 recovery_root -
mount /dev/mapper/recovery_root ./chroot
```

2. Recover your data from the ./chroot folder

3. Unmount the linuxloops rootfs:

```
umount ./chroot
cryptsetup luksClose recovery_root
losetup -d "$image"
```

</details>

<!-- Reference Links -->
<!-- Badges -->
[license-shield]: https://img.shields.io/github/license/sebanc/linuxloops?label=License&logo=Github&style=flat-square
[license-url]: ./LICENSE
[issues-shield]: https://img.shields.io/github/issues/sebanc/linuxloops?label=Issues&logo=Github&style=flat-square
[issues-url]: https://github.com/sebanc/linuxloops/issues
[discord-shield]: https://img.shields.io/badge/Discord-Join-7289da?style=flat-square&logo=discord&logoColor=%23FFFFFF
[discord-url]: https://discord.gg/x2EgK2M
