---
title: Ayudante CachyOS chroot
description: Herramienta para facilitar el chroot en sistemas
---

[**`cachy-chroot`**](https://github.com/CachyOS/cachy-chroot) es un programa auxiliar sencillo para facilitar el proceso de hacer chroot en una instalación existente de CachyOS o cualquier sistema basado en Arch. Lista todas las particiones detectadas en la máquina y también permite listar subvolúmenes BTRFS.
Por último, pero no menos importante, `cachy-chroot` también admite sistemas cifrados mediante LUKS. Mapeará cada entrada de `fstab` con su correspondiente entrada de `crypttab` y cerrará todos los volúmenes LUKS correctamente al salir del chroot.

## Uso

El proceso de chroot **debe** realizarse desde una ISO en vivo. A continuación se muestra un ejemplo de uso de `cachy-chroot` en una instalación BTRFS de CachyOS.

```sh title="chroot con cachy-chroot"
❯ sudo su # Entrar como usuario root dentro de la ISO en vivo
❯ pacman -Sy cachy-chroot # Asegurar que cachy-chroot está en la última versión
❯ cachy-chroot
Info: Found 3 block devices
Info: Found partition: Partition: /dev/nvme0n1p1: FS: vfat UUID: EDA6-ED98
Info: Found partition: Partition: /dev/nvme0n1p2: FS: btrfs UUID: b09a027e-a61d-424f-858f-2e02be61b342
Info: Found partition: Partition: /dev/nvme0n1p4: FS: btrfs UUID: 66e84339-8c77-4131-afce-50ec2cf67a80
? Select the block device for the root partition (use arrow keys):  ›
  Partition: /dev/nvme0n1p1: FS: vfat UUID: EDA6-ED98
❯ Partition: /dev/nvme0n1p2: FS: btrfs UUID: b09a027e-a61d-424f-858f-2e02be61b342
  Partition: /dev/nvme0n1p4: FS: btrfs UUID: 66e84339-8c77-4131-afce-50ec2cf67a80
✔ Select the block device for the root partition (use arrow keys):  · Partition: /dev/nvme0n1p2: FS: btrfs UUID: b09a027e-a61d-424f-858f-2e02be61b342
Info: Selected BTRFS partition, mounting and listing subvolumes...
Info: Mounting partition /dev/nvme0n1p2 at /tmp/cachyos-chroot-temp-mount-b09a027e-a61d-424f-858f-2e02be61b342-hwAeIm with options: []
Info: Unmounting partition at /tmp/cachyos-chroot-temp-mount-b09a027e-a61d-424f-858f-2e02be61b342-hwAeIm
? Do you want to use CachyOS BTRFS preset to auto mount root subvolume? (y/n) › # Introduce y si estás en CachyOS
```

Después de seleccionar la partición raíz, el programa solicitará montar particiones adicionales, por ejemplo, la partición `/boot`

```sh title="Montaje de particiones adicionales"
✔ Do you want to mount additional partitions? · yes
? Enter the mount point for additional partition (e.g. /boot) type 'skip' to cancel:  › # /boot en systemd-boot, /boot/efi en GRUB y rEFInd
```

Al terminar, sal del entorno chroot escribiendo `exit` en el prompt o pulsando `CTRL+D` en el teclado.

```sh title="Salir del chroot"
exit
```

## Más información

- [Arch Wiki - chroot](https://wiki.archlinux.org/title/Chroot)
