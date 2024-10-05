<div id="top"></div>

<!-- Shields/Logos -->
[![License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Discord][discord-shield]][discord-url]
  
# Data recovery from an image

If something goes wrong (or for some other reason), you might want to recover data from a linux loop image while booting from another Linux install, a Linuxloops image or from a Linux live usb.  

<details>
  <summary>Recover data from an unencrypted Linuxloops image</summary>

1. Run the following commands to mount the Linuxloops rootfs:  
```
mkdir -p ./linuxloops_root
image=$(losetup -fP --show <path_to_the_linuxloops_image>)
mount "$image"p3 ./linuxloops_root
```

2. Recover your data from the ./linuxloops_root folder  

3. Unmount the Linuxloops rootfs:  

```
umount ./linuxloops_root
losetup -d "$image"
```

</details>

<details>
  <summary>Recover data from an encrypted Linuxloops image</summary>

1. Run the following commands to mount the Linuxloops rootfs:  
```
mkdir -p ./linuxloops_root
image=$(losetup -fP --show <path_to_the_linuxloops_image>)
cryptsetup luksOpen "$image"p3 recovery_root
mount /dev/mapper/recovery_root ./linuxloops_root
```

2. Recover your data from the ./linuxloops_root folder  

3. Unmount the Linuxloops rootfs:  

```
umount ./linuxloops_root
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

