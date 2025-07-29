---
title: Montaje automático de unidades adicionales mediante fstab al arrancar
description: Monta unidades estáticas adicionales al arrancar utilizando el archivo ubicado en /etc/fstab
---

Este tutorial describirá los conceptos básicos para utilizar el archivo fstab ubicado en /etc/ con el fin de montar unidades estáticas durante el arranque. Explicará brevemente cómo encontrar el UUID de una partición o unidad, qué hacen algunas opciones y proporcionará información adicional en caso de que la información proporcionada sea insuficiente.

## Requisitos previos
- Acceso root

## Añadir entradas a /etc/fstab

### 1. Listar los UUIDs de tus particiones
En el emulador de terminal de tu elección (Konsole, Alacritty, Kitty, etc.) ejecuta lo siguiente:

```sh
❯ lsblk -f
NAME        FSTYPE FSVER LABEL UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
zram0                                                                              [SWAP]
nvme0n1
├─nvme0n1p1 vfat   FAT32       E04D-9F05
├─nvme0n1p2
├─nvme0n1p3 ntfs               08A24E90A24E81E4                      715.4G    50%
├─nvme0n1p4 vfat   FAT32       E09C-D4DA                             628.1M    39% /boot
├─nvme0n1p5 ext4   1.0         187a9f06-9411-48d9-b941-f03c2e605812  203.6G    47% /
└─nvme0n1p6 ntfs
```

En nuestro ejemplo, sabemos que queremos montar una partición de Windows, que es ntfs, y sabemos que aproximadamente la mitad de su espacio está disponible. Por lo tanto, podemos determinar que la partición que queremos montar es `nvme0n1p3` y su UUID es `08A24E90A24E81E4`, con un sistema de archivos `ntfs` en este ejemplo.

### 2. Identificar tu partición

A menudo `lsblk -f` proporcionará toda la información que necesitas para montar tu disco mediante /etc/fstab en este punto. Si encuentras que la información es insuficiente, puedes ejecutar lo siguiente:

```sh
❯ sudo fdisk -l
Device              Start        End    Sectors  Size Type
/dev/nvme0n1p1       2048     206847     204800  100M EFI System
/dev/nvme0n1p2     206848     239615      32768   16M Microsoft reserved
/dev/nvme0n1p3     239616 2997384182 2997144567  1.4T Microsoft basic data
/dev/nvme0n1p4 2997385216 2999482367    2097152    1G EFI System
/dev/nvme0n1p5 2999482368 3905454079  905971712  432G Linux root (x86-64)
/dev/nvme0n1p6 3905454080 3907026943    1572864  768M Windows recovery environment
```

Ya conocemos nuestro UUID en este ejemplo, sin embargo, `fdisk -l` puede hacerlo un poco más claro al mostrarnos el tamaño exacto de la partición (1.4T) así como su tipo (Microsoft basic data).

Esto debería dejarnos absolutamente claro que la partición que queremos es `nvme0n1p3` con un UUID de `08A24E90A24E81E4` como se describió anteriormente. Ya lo sabíamos, pero ahora lo sabemos con seguridad.

Una vez que estés seguro de haber encontrado la partición correcta, copia el UUID. Copiar desde el emulador de terminal normalmente se hace con `ctrl+shift+C`.

### 3. Añadir una entrada a /etc/fstab

Ahora que hemos obtenido el UUID de nuestra partición, es hora de abrir el archivo fstab.

Puedes usar el editor de texto de tu elección; en este ejemplo usaremos nano. Para editar el archivo fstab, debe abrirse como root:

```sh
❯ sudo nano /etc/fstab
```

Usando las teclas de flecha, navega hasta el final del archivo fstab, y luego en una nueva línea crearemos nuestra nueva entrada:

```sh
UUID=08A24E90A24E81E4 /media/windows ntfs3 defaults,nofail 0 0
```
El desglose de esta entrada es el siguiente:

- `UUID=08A24E90A24E81E4` Este es el sistema de archivos que queremos montar, identificado por su UUID. Hay otros métodos para identificar tu sistema de archivos, aunque UUID suele ser el más seguro. Métodos adicionales listados [aquí](https://wiki.archlinux.org/title/Fstab#Identifying_file_systems).

- `/media/windows` El [Estándar de Jerarquía del Sistema de Archivos Linux](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html) dice que `/media/` es la ubicación adecuada para montar unidades extraíbles. `windows` indica el directorio donde queremos montar nuestra unidad. Cada unidad que queramos montar necesitará su propio directorio.

- `ntfs3` Este es el tipo de sistema de archivos para nuestro sistema de archivos. Estamos usando explícitamente el controlador de kernel ntfs3 en nuestro ejemplo. Otros ejemplos serían `ext4`, `xfs` o similares. Esta declaración explícita del tipo de sistema de archivos puede reemplazarse con `auto` para permitir que el comando mount haga su mejor conjetura.

- `defaults,nofail` Las opciones que queremos pasar al comando mount para esta unidad. `nofail` significa que si esta unidad no se puede montar, no causará un error durante el arranque. El arranque continuará normalmente. `defaults` implica un conjunto estándar de opciones lógicas. Típicamente `rw`, `ro` o similares.

- `el primer 0` dump, esto típicamente está obsoleto en sistemas modernos. Dejar esto en 0 no causará ningún problema. Puedes leer más al respecto [aquí](https://linux.die.net/man/8/dump).

- `el segundo 0` Esto establece el orden para las comprobaciones del sistema de archivos al arrancar. Para una partición raíz (a menos que tu sistema de archivos raíz sea btrfs o xfs, que deberían configurarse a 0) esto debería ser 1. Todos los demás sistemas de archivos en tu fstab deberían ser 0 (desactivados) o 2. Más información [aquí](https://man.archlinux.org/man/fsck.8).

Las opciones se explican [aquí](https://man7.org/linux/man-pages/man5/fstab.5.html) y [aquí](https://man7.org/linux/man-pages/man8/mount.8.html) con mucho más detalle.

#### Más información
Como nota adicional, todas las opciones después de la declaración del tipo de sistema de archivos son opcionales si no las cambias de las predeterminadas.

Por lo tanto

`UUID=<UUID de la partición> /media/foo algúnsistema`

y

`UUID=<UUID de la partición> /media/foo algúnsistema defaults 0 0`

son equivalentes. `algúnsistema` seguido de nada es implícitamente `algúnsistema defaults 0 0`

#### Importante para particiones de Windows

Si estás siguiendo esta guía con una partición de Windows, tus opciones deberían ser `uid=1000,gid=1000,rw,user,exec,umask=000` reemplazando uid y gid con tu ID de usuario y grupo. Si no das permisos de usuario y exec, Windows puede bloquear tu unidad dejándote incapaz de modificar cualquier cosa. Esto puede ocurrir independientemente de los permisos si no desactivas el arranque rápido.

Si no estableces umask=000, algunos archivos pueden no ser modificables dependiendo de los permisos.

### 4. Finalizar

Si deseas montar ahora mismo la unidad para la que creaste una entrada, necesitas ejecutar lo siguiente:

```sh
❯ sudo systemctl daemon-reload
```

y luego:

```sh
❯ sudo mount -a
```

Tu unidad debería aparecer ahora en `/media/windows`, y aparecerá allí la próxima vez que arranques, así como en el futuro.

```sh
❯ ls /media/windows
'$Recycle.Bin'             Linux                  SteamLibrary
 AMD                       Modding                swapfile.sys
 Apps                      pagefile.sys          'System Volume Information'
 bootTel.dat               PerfLogs               Users
 Development               ProgramData            WiiU
'Documents and Settings'  'Program Files'         Windows
 DumpStack.log.tmp        'Program Files (x86)'   XboxGames
 FanControl                Recovery               xiv_modding
 Games                     RetroArch-Win64
 Intel                    'Ship of Harkinian'
 ```

 Si deseas crear un enlace a tu unidad recién montada en tu directorio home, puedes ejecutar lo siguiente:

 ```sh
 ❯ ln -s /media/windows ~/Windows
 ```

 Para comprobar que funcionó:

 ```sh
 ❯ ls ~/Windows
 '$Recycle.Bin'             Linux                  SteamLibrary
 AMD                       Modding                swapfile.sys
 Apps                      pagefile.sys          'System Volume Information'
 bootTel.dat               PerfLogs               Users
 Development               ProgramData            WiiU
'Documents and Settings'  'Program Files'         Windows
 DumpStack.log.tmp        'Program Files (x86)'   XboxGames
 FanControl                Recovery               xiv_modding
 Games                     RetroArch-Win64
 Intel                    'Ship of Harkinian'
 ```


## Resumen

- Encuentra el UUID de tu partición
```sh
lsblk -f
```

- Abre /etc/fstab
```sh
sudo nano /etc/fstab
```

- Crea una entrada al final del archivo
```sh
UUID=<UUID de la partición> /media/foo algúnsistema defaults 0 0
```
Reemplazando `<UUID de la partición>`, `foo`, y `algúnsistema` con tu UUID, directorio y sistema de archivos, por ejemplo, ext4, así como estableciendo cualquier otra opción que puedas querer después de defaults, como `_netdev` para un NAS, o `nofail` para cualquier unidad no crítica.

- Recarga tu daemon

```sh
❯ sudo systemctl daemon-reload
```

- Monta tu unidad
```sh
❯ sudo mount -a
```

Esta unidad ahora está montada, y se montará automáticamente al arrancar a partir de ahora.

## Lectura adicional
- https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html - Estándar de Jerarquía del Sistema de Archivos
- https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch03s11.html - FHS sobre `/media/`
- https://linux.die.net/man/8/dump - manual para `dump`
- https://man.archlinux.org/man/fsck.8 - manual para `fsck`
- https://man.archlinux.org/man/fstab.5.en - página del manual para fstab
- https://wiki.archlinux.org/title/Fstab - Wiki de Arch Linux para fstab
