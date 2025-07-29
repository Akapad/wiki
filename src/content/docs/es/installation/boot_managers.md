---
title: Gestores de arranque ofrecidos
description: Descripción y recomendaciones para los gestores de arranque disponibles actualmente
---

Para ofrecer la mejor experiencia en diversos dispositivos, CachyOS actualmente ofrece los siguientes gestores de arranque: systemd-boot, rEFInd, GRUB y Limine.
Este artículo de la wiki describirá las características de cada gestor de arranque e incluye nuestras recomendaciones para elegir entre ellos. Para
configuración, consulta [Configuración del Gestor de Arranque](/configuration/boot_manager_configuration).

## systemd-boot

Como parte de la familia systemd, systemd-boot fue creado para ser lo más sencillo posible, por lo tanto solo tiene soporte para sistemas basados en UEFI. Este diseño simple pero eficiente asegura que sea fiable y rápido. Sin embargo, esto viene a costa de las características avanzadas que ofrecen otros gestores de arranque.

### Ventajas
- Configuración muy sencilla.
- Las entradas de arranque están separadas en múltiples archivos, lo que facilita su gestión.

### Desventajas
- Carece de soporte adecuado para BIOS/MBR.
- Diseño muy básico y carece de cualquier tipo de tema o personalización.
- La configuración no se genera automáticamente a menos que se configure para hacerlo. CachyOS incluye un gestor para systemd-boot que ofrece configuración generada automáticamente.
- Solo puede leer imágenes de arranque en sistemas de archivos compatibles con EFI (FAT, FAT16, FAT32).
- Incapacidad para encontrar imágenes de arranque en particiones distintas a la suya propia.
- No soporta adecuadamente la reversión a instantáneas de Btrfs debido al requisito de almacenar imágenes del kernel en la partición de arranque en lugar del sistema de archivos raíz.

### Recomendación

Systemd-boot es el gestor de arranque recomendado y predeterminado para CachyOS. Elige este si no estás seguro.

## rEFInd

Como bifurcación de rEFIt, rEFInd se creó principalmente para facilitar el arranque múltiple a usuarios de MacOS. Sin embargo, rEFInd ha evolucionado para ser independiente del hardware, convirtiéndolo en una gran opción para el arranque múltiple en cualquier sistema. Lo más destacado de rEFInd es su capacidad para escanear todos los dispositivos de almacenamiento durante el arranque y mostrar entradas para cada SO/Kernel encontrado.

### Ventajas

- Detección automática de todos los sistemas operativos y kernels en los dispositivos de almacenamiento.
- Poca o ninguna configuración requerida debido a la mencionada detección automática.
- Interfaz de usuario mucho más gráfica que recuerda al selector de arranque de MacOS.
- Gran soporte para temas.
- Soporte opcional para pantalla táctil.
- Capaz de leer imágenes de arranque desde sistemas de archivos EFI (FAT, FAT16, FAT32), así como EXT4 y BTRFS. El soporte para otros sistemas de archivos se puede añadir mediante la instalación de controladores EFI del paquete ``efifs``.

### Desventajas

- No soporta sistemas BIOS.

### Recomendación

rEFInd es el gestor de arranque recomendado para arrancar con múltiples sistemas operativos.

## GRUB

GRUB es el más antiguo de los gestores de arranque disponibles. Tiene un conjunto de características muy amplio, funciona en casi cualquier máquina y es el gestor de arranque para Linux más comúnmente utilizado. A continuación se muestra una lista de sus principales ventajas y desventajas.

### Ventajas
- Capaz de leer imágenes de arranque desde casi todos los sistemas de archivos Linux disponibles.
- Ampliamente utilizado y muy fácil encontrar información en línea.
- Capaz de descifrar particiones de arranque cifradas.
- El único cargador de arranque ofrecido que permite arrancar máquinas BIOS.
- Aspecto anticuado. Sin embargo, tiene gran soporte para temas para compensarlo.

### Desventajas
- Sobrecargado debido a la necesidad de dar soporte a hardware mucho más antiguo y a la necesidad de controladores para muchos sistemas de archivos.
- Notablemente más lento en comparación con systemd-boot, rEFInd y Limine.

### Recomendación

GRUB es el único gestor de arranque que soporta el cifrado de la partición de arranque (diferente del cifrado de disco).

## Limine

Limine es un cargador de arranque multiprotocolo moderno, avanzado y portable. Sirve como implementación de referencia para el protocolo de arranque Limine y soporta el arranque de Linux, así como la carga encadenada de otros cargadores de arranque.

### Ventajas

- Soporta múltiples protocolos de arranque, incluyendo Multiboot2 y los protocolos de arranque de Linux.
- Puede arrancar tanto en sistemas UEFI como BIOS, haciéndolo versátil para diferentes configuraciones de hardware.
- Tiene capacidades de personalización similares a GRUB.
- Soporte directo para instantáneas Btrfs, que está habilitado por defecto para instalaciones que usan Btrfs como sistema de archivos.

### Desventajas

- Solo soporta algunos sistemas de archivos, como FAT12, FAT16, FAT32 e ISO9660 para la partición `/boot`, lo que puede requerir configuración adicional para sistemas que usan otros sistemas de archivos.
- A diferencia de otros cargadores de arranque, Limine no añade automáticamente una entrada a la NVRAM en sistemas UEFI; esto debe hacerse manualmente usando herramientas como `efibootmgr` o gestionarse mediante `limine-entry-tool`, que viene preinstalada en CachyOS.

### Recomendación

Limine es recomendado para usuarios que necesitan un cargador de arranque ligero y versátil que soporte tanto sistemas UEFI como BIOS. Es particularmente adecuado para aquellos que prefieren una configuración simple con opciones de personalización y soporte para instantáneas Btrfs. Además, Limine sirve como un reemplazo moderno para GRUB, que ha visto menos actualizaciones recientemente y ha enfrentado múltiples problemas de seguridad debido a sus controladores EFI/sistema de archivos.

## Resumen

Elige **Limine** para la mayoría de usuarios: ofrece una configuración fácil con soporte incorporado para instantáneas BTRFS, funciona en sistemas BIOS y UEFI, y maneja bien el arranque múltiple con Windows. Elige **GRUB** solo si necesitas específicamente soporte para partición de arranque cifrada. Considera **rEFInd** si priorizas una interfaz gráfica pulida y principalmente arrancas múltiples sistemas en UEFI. Elige **systemd-boot** si quieres la configuración más sencilla y no necesitas soporte para instantáneas BTRFS listo para usar.
