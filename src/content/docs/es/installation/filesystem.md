---
title: Sistemas de archivos
description: Descripción y recomendaciones para los sistemas de archivos disponibles. (ext4, f2fs, btrfs, xfs, zfs, bcachefs)
---

CachyOS ofrece 5 sistemas de archivos para permitir al usuario elegir el que mejor se adapte a sus necesidades. A continuación se detallan las ventajas, desventajas y recomendaciones para cada sistema de archivos. Cada sistema de archivos viene con sus requisitos/utilidades preinstalados en CachyOS.

:::note
BTRFS es el sistema de archivos predeterminado y recomendado para CachyOS. Elígelo si no estás seguro.
:::

## XFS
XFS es un sistema de archivos con registro (journaling) creado y desarrollado por Silicon Graphics, Inc. Fue creado en 1993, portado a Linux en 2001, y ahora es ampliamente compatible con la mayoría de las distribuciones de Linux.
### Ventajas
- Rápido, XFS fue diseñado originalmente pensando en la velocidad y la escalabilidad extrema.
- Fiable, XFS utiliza varias tecnologías para prevenir la corrupción de datos.
- Resistente a la fragmentación debido a su naturaleza basada en extensiones y su estrategia de asignación retardada.
### Desventajas
- No se puede reducir su tamaño.

### Utilidad para el usuario
El paquete que contiene las herramientas de usuario para gestionar sistemas de archivos XFS es `xfsprogs`.

### Recomendación:
XFS es el sistema de archivos recomendado para usuarios que no necesitan funciones avanzadas y simplemente quieren un sistema de archivos rápido y fiable.


## BTRFS
BTRFS es un sistema de archivos moderno de copia en escritura (COW) creado en 2007 y declarado estable en el kernel de Linux en 2013. Es ampliamente compatible y principalmente conocido por su conjunto de características avanzadas.
### Ventajas
- Compresión transparente. BTRFS permite comprimir archivos de forma transparente para ahorrar espacio significativo sin intervención del usuario. CachyOS viene con compresión ZSTD configurada en nivel 3 por defecto.
- Funcionalidad de instantáneas. BTRFS aprovecha su naturaleza COW para permitir la creación de instantáneas de subvolúmenes que ocupan muy poco espacio real.
- Funcionalidad de subvolúmenes que permite un mayor control sobre el sistema de archivos.
- Capaz de crecer o reducirse.
- Desarrollo muy rápido.
### Desventajas
- A veces requiere desfragmentación o equilibrado.
- Peor rendimiento en discos rotacionales debido a la fragmentación mencionada.
### Utilidad para el usuario
El paquete de utilidades para BTRFS es `btrfs-progs`

### Estructura de subvolúmenes
CachyOS proporciona una estructura de subvolúmenes lista para usar que permite una fácil funcionalidad de instantáneas.
- Subvol @ = /
- Subvol @home = /home
- Subvol @root = /root
- Subvol @srv = /srv
- Subvol @cache = /var/cache
- Subvol @tmp = /var/tmp
- Subvol @log = /var/log

### Recomendación:
BTRFS es recomendado para usuarios que desean funcionalidad de instantáneas/copias de seguridad y compresión transparente.


## EXT4
EXT4 (cuarto sistema de archivos extendido) es el sistema de archivos más comúnmente utilizado en Linux. EXT4 se estabilizó en el kernel de Linux en 2008.
### Ventajas
- Muy común, lo que permite fácil acceso a numerosos recursos.
- Fiable. EXT4 tiene un historial probado de gran fiabilidad.
- Capaz de crecer o reducirse.
### Desventajas
- Construido sobre una base de código antigua.
- Carece de muchas de las características avanzadas que ofrecen otros sistemas de archivos.

### Utilidades para el usuario
El paquete para gestionar ext4 es `e2fsprogs`

### Recomendación:
EXT4 es recomendado para usuarios que desean el sistema de archivos más simple y comúnmente utilizado.


## ZFS

ZFS es un sistema de archivos avanzado desarrollado originalmente por Sun Microsystems en 2005. ZFS tiene muchas características, sin embargo, está licenciado bajo CDDL, lo que significa que no puede incluirse dentro del kernel de Linux y requiere un módulo separado instalado.

:::caution
No utilices un kernel en tiempo real junto con ZFS porque no es compatible debido a problemas de licencia.
:::

### Ventajas
- Almacenamiento en pool (zpool)
- Instantáneas usando COW
- Compresión
- Soporte para Raid-Z
- La caché ARC permite tiempos de lectura increíblemente rápidos en archivos de acceso frecuente.
### Desventajas
- Muy complicado de usar y entender debido a características como zpool y ARC.
- ARC requiere mucha RAM para ser efectivo.
- No incluido en el kernel de Linux, por lo tanto depende de un módulo de kernel de terceros (OpenZFS)
- Incompatible con la preempción en tiempo real

### Herramientas necesarias
'ZFS-Module' CachyOS proporciona un módulo zfs precompilado para cada versión del kernel.
`zfs-utils` para las utilidades de usuario.

### Recomendación:
ZFS solo debe ser utilizado por usuarios avanzados que desean las características avanzadas de ZFS como el almacenamiento en pool o la caché ARC.


## F2FS
F2FS o Sistema de Archivos Amigable con Flash, es un sistema de archivos flash creado y desarrollado por Samsung originalmente para el kernel de Linux. F2FS fue creado para adaptarse específicamente a la memoria flash NAND utilizada en el almacenamiento moderno.
### Ventajas
- Diseñado pensando en la compatibilidad con memoria flash.
- Compresión transparente utilizada para reducir las escrituras en disco (el ahorro de espacio no es actualmente utilizable por el usuario)
- Más rápido que otros sistemas de archivos como EXT4.
- Mejor nivelación de desgaste, prolongando aún más la vida de la memoria flash NAND.
### Desventajas
- No se puede reducir su tamaño.
- El ahorro de espacio por compresión no puede ser utilizado actualmente por el usuario. Esto podría añadirse en el futuro.
- Fsck (verificación del sistema de archivos) relativamente débil.
- Degradar a un kernel más antiguo que la versión que creó el sistema de archivos puede causar problemas.

### Utilidades para el usuario
La utilidad principal para f2fs es `f2fs-tools`

### Recomendación:
F2FS solo se recomienda para usuarios que desean maximizar la vida útil de su memoria flash NAND.

## BcacheFS
Bcachefs es un nuevo sistema de archivos avanzado para Linux, con énfasis en la fiabilidad y robustez, y el conjunto completo de características que se esperarían de un sistema de archivos moderno.

:::caution[ATENCIÓN]
Bcachefs todavía se considera experimental y puede tener problemas.
:::

### Ventajas
- Copia en escritura (CoW) - como BTRFS o ZFS
- Compresión
- Caché, Colocación de datos
- Replicación
- Escalable
### Desventajas
- Experimental
- La configuración puede ser complicada

## Resumen
Utiliza el sistema de archivos predeterminado **BTRFS** ya que se considera estable y tiene muchas características interesantes (instantáneas, compresión, etc.). Utiliza **XFS** o **EXT4** para un sistema de archivos simple y rápido.

