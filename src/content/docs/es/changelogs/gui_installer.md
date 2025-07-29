---
title: Registros de cambios del instalador GUI
description: Registros de cambios de Calamares y la ISO Live con GUI
---
25.07
----
**Características:**
-   **Shell**: El shell del usuario ahora se puede elegir durante la instalación entre fish, zsh y bash. Fish sigue siendo la opción predeterminada.
-   **chwd**: Instala plasma-x11 para controladores NVIDIA antiguos
-   **Netinstall**: Se añadió fwupd a KDE Plasma y Gnome
-   **mesa-git**: Se añadió soporte para AMD Anti Lag
-   **firefox**: Se introdujo una alternativa llamada "firefox-pure", que incluye mejoras con el perfil userjs. Además, se ha añadido "cachyos-firefox-settings", que se puede instalar sobre firefox.
-   **Proton-CachyOS**:
  -   Importados commits de wine-wayland
  -   Añadida la variable de entorno "PROTON_FSR4_UPGRADE", que descargará automáticamente la última DLL de FSR4 y la reemplazará para una actualización automática en juegos compatibles con FSR 3.1
  -   Añadidos muchos parches relacionados con Wayland del Wine upstream que se lanzaron después de Wine 10.0
  -   Añadidos parches para ayudar con una mejor integración de anticheat. Gracias a NelloKudo
  -   Añadidos parches para AMD's Anti Lag 2 para vkd3d-proton y wine
  -   Actualizado umu-protonfixes al último commit

**Correcciones:**
-   **Keyring**: Mejorado el manejo de la instalación del keyring para evitar problemas y realizar varios reintentos.
-   **systemd-oomd**: Desactivado systemd-oomd, ya que tenía problemas junto con le9 y cerraba aplicaciones demasiado pronto

**Registro de cambios para la Edición Handheld:**
-   **handheld-settings**: Importados varios ajustes de SteamOS a la Edición Handheld
-   **pipewire**: Establecido quantum mínimo a 256
-   **SteamDeck-OLED**: Instalación de galileo-mura para Steam Deck OLED
-   **Lenovo Legion Go S**: Añadido soporte para Lenovo Legion Go S

25.05
----
**Características:**
-   **ISO**: Añadida detección automática durante el arranque de la ISO para identificar la GPU NVIDIA del sistema y cargar el módulo apropiado (p. ej., nvidia-open, nvidia), proporcionando mejor soporte para series 10xx y anteriores.
-   **Plymouth**: Añadida una nueva animación de Plymouth.
  -   Gracias a Eren ([https://github.com/erenyldz89](https://github.com/erenyldz89)) por trabajar en esto!
-   **Navegador**: Cachy-Browser ha sido deprecado. Ahora proporcionamos Firefox como navegador preinstalado por defecto. Hay una guía para migrar perfiles a Firefox (y sus derivados) aquí: [https://wiki.cachyos.org/support/faq/#migrating-your-profile-from-cachy-browser-to-firefox](https://wiki.cachyos.org/support/faq/#migrating-your-profile-from-cachy-browser-to-firefox)
-   **netinstall**: Añadidos kcalc, filelight, plymouth-kcm y kio-admin a la instalación de KDE.
-   **mkinitcpio**: Desactivado el initramfs de respaldo por defecto. Esto ahorrará una cantidad significativa de espacio.
-   **Mirrors**: Añadido un nuevo mirror de 10 Gbps en Bangladesh. ¡Gracias a Limda por alojarlo!
-   **Proton**:
  -   Rebasados casi todos los parches de **Proton CachyOS 9.0**.
  -   Habilitado el driver de Wayland para compilaciones Steam Linux Runtime. Activar con `PROTON_ENABLE_WAYLAND=1`. Gracias a [GloriousEggroll](https://github.com/GloriousEggroll) por hacerlo posible.
  -   Añadidos muchos parches relacionados con Wayland del Wine upstream lanzados después de Wine 10.0.
  -   Corregidos varios problemas con el driver de Wayland y juegos Vulkan. Gracias a [Etaash-mathamsetty](https://github.com/Etaash-mathamsetty) por todo el arduo trabajo.
  -   Añadida una implementación provisional para `amdxc64.dll` para habilitar FSR4. Usa `FSR4_UPGRADE=1` para actualizar juegos FSR3.1 a FSR4. Gracias de nuevo a [Etaash-mathamsetty](https://github.com/Etaash-mathamsetty). Instrucciones: [https://github.com/Etaash-mathamsetty/wine-builds/releases/tag/fsr4](https://github.com/Etaash-mathamsetty/wine-builds/releases/tag/fsr4)
  -   Añadidos parches relacionados con DualSense para una detección más completa de dispositivos de audio para háptica basada en sonido por cable. Algunos juegos que dependían de ese comportamiento específico ahora deberían tener esa funcionalidad. Gracias a [ClearlyClaire](https://github.com/ClearlyClaire) por los parches originales y [Exotic0015](https://github.com/Exotic0015) por investigarlo desde **Proton CachyOS 9.0**. Upstream: [https://gitlab.winehq.org/wine/wine/-/merge_requests/7238](https://gitlab.winehq.org/wine/wine/-/merge_requests/7238)
  -   Eliminado el parche de Dragon Age Inquisition ya que no funcionaba. Por favor, usa **Proton CachyOS 9.0** por ahora con ese juego.
-   **GRUB**: Añadido un nuevo tema para GRUB. Gracias a [diegons490](https://github.com/diegons490/cachyos-grub-theme).

**Correcciones:**
-   **Mirrors**: Solucionado un problema donde los usuarios de Rusia ya no podían instalar. Esto se mitigó al no usar CDN77, que Rusia había comenzado a bloquear.
-   **kde-settings**: Deshabilitado el icono de Discover en la barra de tareas.
-   **ddcutil**: Publicada la versión preliminar de ddcutil 2.2.1 para solucionar un problema donde las GPUs AMD se congelaban al ver vídeos de YouTube.

**Registro de cambios para la Edición Handheld:**
-   **os-branch**: El Modo Juego ahora muestra correctamente que se está utilizando CachyOS Linux.
-   **audio**: Actualizados los perfiles de convolver.
-   **steamos-manager**: Se utiliza para la gestión de reloj de GPU y TDP, actualizaciones de BIOS/dock, mantenimiento de dispositivos de almacenamiento, formateo de almacenamiento externo y límite de carga de batería para Steam Deck.
-   **steamos-powerbuttond**: Este componente reemplaza el powerbuttond estándar para una mejor experiencia de suspensión.
-   **jupiter-hw-support**: Actualizado a 20250501.

25.04
----

**Características:**
- **occt**: Añadido OCCT a la ISO para tener un entorno en vivo para pruebas de estrés
  - ¡Gracias a Marek por proporcionar esta idea!

**Correcciones:**
- **kernel**: Corregido el fallo de módulo en portátiles Asus
- **limine**: Limine ahora tiene mkinitcpio-limine-hook instalado y creará automáticamente entradas del gestor de arranque


**Registro de cambios para la Edición Handheld:**
- **audio**: Añadidos perfiles de audio para ROG Ally X y Legion Go
- **gamescope**: Reemplazado gamescope-plus con gamescope upstream

25.03
----

**Características**:
- **Gestor de arranque**: Añadido soporte para el gestor de arranque Limine
- **Gestor de arranque**: Añadido soporte para instantáneas automáticas para el gestor de arranque Limine
- **Samba**: Añadido paquete "cachyos-samba-settings" para configurar fácilmente un punto de montaje Samba
- **NVIDIA**: Reactivado el firmware GSP para el módulo cerrado de NVIDIA
- **Kernel**: Añadido soporte para el controlador Asus Armoury
- **Secure Boot**: Mejorado el script "sbctl-batch-sign" para firmar solo los archivos deseados
- **udev**: Revertido el uso de ntfs3 como controlador predeterminado para particiones NTFS
  - Información: Usar el controlador de Kernel NTFS3 como predeterminado causó problemas para algunos usuarios. Por lo tanto, lo hemos revertido.
- **wine**: Wine y Wine-Staging ahora usan WoW64 y NTSync por defecto
- **scx-manager**: Movido el administrador GUI de sched-ext del Administrador de Kernel a su propia aplicación
- **Soporte de Hardware**: Añadido soporte para RDNA4, RTX 5070 Ti y 5070
- **Ajustes**: Añadido soporte para DLSS Swapper - este es un script que actualiza y usa automáticamente la última versión y preajuste de dlss
- **Actualizaciones de paquetes**: linux-cachyos 6.14.0, NVIDIA 570.133.07, Gnome 48, Plasma 6.3.3, mesa 25.0.2, linux-api-headers 6.14.0, linux-tools 6.14.0

**Correcciones**:
- **initcpiocfg**: Eliminada la adición del módulo "crc32c-intel" a mkinitcpio - Ha sido obsoleto y ahora se usa por defecto el módulo "crc32c"
- **chwd**: MacBook T2 desactivar la descarga del brcmfmac
- **chwd**: No instalar el controlador NVIDIA 390.xx para portátiles

25.02
----

**Características**:
- **Kernel**:
  - La optimización Propeller ahora se aplica al kernel **linux-cachyos** predeterminado para todas las arquitecturas disponibles.
  - **Nota**: En combinación con AutoFDO, esto puede mejorar el rendimiento alrededor de un 10%, dependiendo de la carga de trabajo.
- **NVIDIA**: Añadido soporte para la arquitectura Blackwell.
- **ISO**: Usando el módulo nvidia-open como predeterminado para proporcionar soporte a Blackwell. Los usuarios con GPUs más antiguas que Turing deberían usar la primera opción de arranque o la opción de respaldo.
- **Ajustes**: Habilitado tap-to-click para sesiones X11 por defecto.
- **udev**: Usar ntfs3 como controlador predeterminado para particiones NTFS.
- **game-performance**: Desactivado el protector de pantalla mientras se ejecutan juegos.
- **kernel-manager (sched-ext)**: Añadido soporte para modo servidor.
- **kernel**: Añadidas correcciones para la función de núcleo preferido de AMD.
- **chwd**: Vuelto a añadir la solución temporal para RTD3.
- **Actualizaciones de paquetes**: linux-cachyos 6.13.0, NVIDIA 570.86.16, LLVM 19, glibc 2.41, mesa 24.3.4.

**Correcciones**:
- **chwd**: Solucionado un problema donde los portátiles híbridos con hardware Intel y NVIDIA no podían usar su GPU en DaVinci Resolve.
- **glibc**: Añadida una corrección para CVE-2025-0395.
- **kernel-manager**: Intentar instalar el módulo NVIDIA precompilado, si está disponible para el kernel Arch predeterminado.
- **kernel-manager**: Añadida una comprobación adicional para evitar sobrescribir el valor en caso de que un módulo no esté disponible.

**Registro de cambios para la Edición Handheld:**
- **hooks**: Permitido el uso de Proton compilado nativamente de nuevo.
- **misc**: Varias actualizaciones y correcciones.

24.12
----

**Características**:
- Kernel:
  - AutoFDO ahora se aplica al kernel predeterminado `linux-cachyos` para todas las arquitecturas disponibles
  - **Nota**: Las mejoras de rendimiento son mínimas por ahora debido a limitaciones actuales. La fusión de perfiles requiere LLVM 19, y la optimización Propeller depende de ello. Anticipamos que LLVM 19 y perfiles más optimizados estarán disponibles a finales de año, tras la adopción de LLVM 19 por parte de Arch Linux
- chwd: Rusticl ahora está configurado correctamente
- chwd: mejorado el registro de errores durante las llamadas a hooks
- chwd: corregida la selección de controladores VAAPI
- cachyos-settings: Añadido un script para facilitar la ejecución de aplicaciones a través de Zink
- Configuración Sysctl: Reelaboradas y optimizadas varias configuraciones
- Kernel Manager: Añadido soporte para `scx_loader`, permitiendo el cambio nativo de programador
- Instalador: El servicio Bluetooth ahora está habilitado por defecto
- Netinstall:
  - Añadido `wireless-regdb` a los paquetes instalados
  - Esto configura la conexión para usar canales apropiados y desbloquea canales adicionales, potencialmente mejorando la velocidad de Internet
  - **Nota**: Una región genérica se establece por defecto; se recomienda personalizarla a tu región para un rendimiento óptimo
- **Actualizaciones de paquetes**: NVIDIA 565.77, linux-cachyos 6.12.6, mesa 24.3.2, scx-scheds 1.0.8, zfs 2.2.7

**Correcciones de errores**
- Instalador: Los registros de instalación ya no generan ventanas de terminal de depuración
- Gestión de particiones:
  - La configuración adecuada de `umask` asegura que `/boot` sea inaccesible sin permisos suficientes
- Iniciar Instalador: Se han corregido las comprobaciones de conectividad a Internet

**Registro de cambios para la Edición Handheld:**
- Actualizados paquetes relacionados con dispositivos portátiles
- Solucionado problema con la gestión de perfiles de energía
- Añadido soporte para WiFi 6

24.11
----

**Características:**
- thp-shrinker: Establecido el valor max_ptes_none a 80% para páginas con ceros. Esto reducirá el uso de memoria cuando se utiliza THP always, manteniendo el mismo rendimiento
- NVIDIA: El firmware GSP ahora se desactiva automáticamente si el usuario cambia por su cuenta al controlador cerrado
- chwd: NVIDIA: el servicio nvidia-powerd se habilita para portátiles, para alcanzar el tdp disponible máximo
- proton-cachyos: La generación de fotogramas DLSS ya funciona. Se espera que también funcione en el futuro en el proton upstream
- kernel: Se ha aplicado el optimizador de caché AMD. Los usuarios con CPUs de doble CCD x3d ahora pueden cambiar entre preferir núcleos de frecuencia o caché
- kernel: amd-pstate: Retroportados arreglos de rendimiento de amd-pstate para Strix Point
- kernel: Añadidas correcciones upstream para los problemas de tdp en GPUs AMD rdna2 y rdna3
- kernel: Añadidas correcciones de sincronización para pantallas con configuración 5120x1440x240
- kernel: Kernel experimental optimizado con AutoFDO disponible en el repositorio como "linux-cachyos-autofdo"
- ISO: Añadida comprobación si el usuario ejecuta la edición handheld y advertirle si está iniciando la instalación en un dispositivo no compatible
- ISO: Añadida comprobación si el usuario está utilizando la última ISO, si no, advertirle

**Correcciones de errores:**
- refind: particionamiento: cambiado de diseño de partición de 3 vías a 2 vías
- netinstall: añadido kdeplasma-addons a la instalación de Plasma
- calamares: Solucionado un problema durante el particionamiento con una partición swap

**Registro de cambios para la Edición Handheld:**
- El soporte para Rog Ally X debería haberse mejorado

24.10
----

**Características:**
- Actualizaciones de paquetes: linux-cachyos 6.11.1, mesa 24.2.4, scx-scheds 1.0.5, python 3.12.7

**Correcciones de errores:**
- sddm: Incorporado sddm más nuevo para arreglar inicios de sesión en sesiones wayland
- ISO: Añadido xf86-video-amdgpu para corregir la carga de sesión gráfica en algunas configuraciones
- chwd: Corregida la reinstalación de perfiles

24.09
----

**Características:**
- Paquetes: Optimizados varios paquetes con PGO, como LLVM, Clang, svt-av1 y nodejs. Esto produjo, por ejemplo, un compilador Clang un 10% más rápido
- Repositorio: El repositorio ahora se sincroniza y actualiza con más frecuencia, lo que significa que habrá aún menos retraso. El intervalo de sincronización se ha reducido de cada 3 horas a cada hora
- Repositorio: A partir del 27.09.2024, los paquetes compilados con -fpic habilitarán automáticamente -fno-semantic-interposition. Esto puede proporcionar una mejora de rendimiento para muchos paquetes
- zlib-ng: Ahora se usa como reemplazo para zlib
- sddm: En la instalación de KDE, sddm ahora usará Wayland como compositor por defecto
- cachyos-settings: NetworkManager ahora usa systemd-resolved como backend, lo que ayuda con el almacenamiento en caché DNS
- cachyos-settings: Usar time.google.com como servidor de sincronización de tiempo para evitar problemas con la sincronización temporal en algunas configuraciones
- gcc: Añadidas correcciones para el ajuste de znver5
- gcc: Parches y flags seleccionados de Clear Linux
- glibc: Añadidos parches "evex" y selecciones de Clear Linux
- wiki: La Wiki recibió muchas nuevas adiciones y reestructuraciones
- chwd: Simplificada la gestión de dispositivos
- chwd: Todos los perfiles están ahora diseñados específicamente para dispositivos PCI
- chwd: Añadido --autoconfigure para manejar automáticamente la instalación del controlador
- Actualizaciones de paquetes: linux-cachyos 6.11.0, mesa 24.2.3, Plasma 6.1.5, NVIDIA 560.35.03, calamares 3.3.10, QT 6.7.3

**Correcciones de errores:**
- Launch-Installer: Añadidas correcciones para sincronizar el reloj del hardware antes de iniciar la instalación
- calamares: Añadida corrección para desmontar el sistema de archivos después de la instalación
- keyring: Limpiar el anillo de claves y recrearlo antes de iniciar la instalación; esto soluciona problemas raros con el anillo de claves
- sysctl: Los volcados de núcleo se han vuelto a habilitar
- chwd: Eliminado `libva-nvidia-driver` del perfil PRIME para evitar posibles conflictos y mejorar la compatibilidad con software como Spectacle
- cachyos-settings: Añadida solución alternativa para fallos de GNOME Wayland
- cachyos-fish/zsh-config: Eliminadas peculiaridades específicas de wayland

**Registro de cambios para la Edición Handheld:**
- Ally/Ally X: HHD ha sido reemplazado con inputplumber, ya que hhd no usa correctamente el controlador del kernel para ello, lo que resulta en problemas
- Actualizados paquetes relacionados con dispositivos portátiles

24.08
----

**Características:**
- chwd: NVIDIA ahora usa el módulo abierto como predeterminado para tarjetas compatibles
- Escritorio: Añadido el entorno de escritorio Cosmic a las opciones de instalación
- NVIDIA: El último controlador beta 560 es ahora el predeterminado; egl-wayland parcheado para corregir fallos en Firefox y otras aplicaciones
- mirrors: CDN77 patrocinó a CachyOS con almacenamiento de objetos con caché mundial, mejorando significativamente las velocidades de conexión para los usuarios
- mirrors: CachyOS ahora proporciona su propio espejo de Arch Linux para evitar problemas de sincronización, establecido como predeterminado durante la instalación junto con espejos de respaldo
- SecureBoot: Introducido script y tutorial en la Wiki para soporte fácil de Secure Boot
- cachy-chroot: Añadido auto-montaje a través de fstab para simplificar el chroot
- cachy-chroot: Implementado soporte para cifrado LUKS
- kernel-manager: Añadido soporte para establecer flags de sched-ext en la configuración de sched-ext
- kernel-manager: Introducida opción para compilar nvidia-open
- kernel-manager: Añadida opción para recordar las últimas opciones utilizadas en la página de configuración
- Actualizaciones de paquetes: linux-cachyos 6.10.5, mesa 24.2.0, Plasma 6.1.4, NVIDIA 560.31.02

**Correcciones de errores:**
- chwd: Mejorada la detección de perfiles PRIME basada en el nombre del dispositivo
- chwd: Eliminada solución temporal para RTD3 debido a problemas en algunas configuraciones
- cachyos-rate-mirrors: Desactivada la clasificación de espejos cuando se ejecuta en Live ISO
- cachy-chroot: Corrige un error cuando una partición no tenía un fstype o uuid válido (ej. Partición de recuperación de Microsoft)
- cachy-chroot: Fixes a crash when a partition didn't have a valid fstype or uuid (eg Microsoft Recovery Partition)
- calamares: Refactored keyring initialization
- kernel-manager: Fixed support for building custom pkgbase with LTO kernels and modules enabled
- kernel-manager: Fixed password prompt delay
- ISO: Replaced radeon.modeset=1 with amdgpu.modeset=1 for modern GPUs
- game-performance: Prevented failure when profile is unavailable

**Changelog for Handheld Edition:**
- device support: Added support for Ally X, thanks to Luke Jones
- libei: Implemented support for libei, replacing libextest
- packagekit: Blocked packagekit installation to prevent issues with system updates via Discover
- hook: Added pacman-hook to conflict with natively compiled Proton versions, avoiding potential issues
- Updated jupiter-fan-control, steamdeck-dsp, and Steam Deck firmware

24.07
----

**Features:**
- Repository: Introduce Zen 4 optimized repository, this will be used for Zen4 and Zen5 CPU's
- ISO: Add automatic architecture check for Zen4/Zen5 repository
- chwd: Added GC support for AMD GPU's, this helps for detecting official ROCm supported GPUs
- chwd: Use libva-nvidia-driver on supported cards
- ksmctl: Introduce tool to enable/disable KSM: ksmctl --enable
- kernel: For the "linux-cachyos" kernel is now a "linux-cachyos-dbg" package available, this contains an unstripped vmlinux for debugging purposes
- kernel: amd cpb boost is now available and the power-profiles-daemon is patched, if the "powersave" profile is set, it will disable the boost on amd cpus
- kernel: Added power saving patch for AMD SoCs for video playback
- kernel-manager: Added support for managing sched-ext schedulers and getting information via GUI
- steam/proton: There is now a "game-performance" script, which can be added to steam's launch options
- power-profiles: On AMD Pstate supported CPUs the lowest Linear frequency is now set higher, this can improve latency and 1% lows
- kwin: Added back-port for tearing, this has been tested. On NVIDIA it only works on native wayland applications
- netinstall: Cutefish has been dropped as installable Desktop Environment
- Mirrors: Added Austria and China Mirror, the China Mirror is hosted by the TUNA University. This should help a lot of users from china
- Package Updates: linux-cachyos 6.9.9, mesa 24.1.3, NVIDIA 555.58.02, Plasma 6.1.2, LLVM 18.1.8

**Bug Fixes:**
- ISO: Set copytoram to auto instead of yes
- ISO: Fixed Sleep on Live ISO for Laptops
- Launch Installer: Install the latest archlinux-keyring, before the installation starts to avoid issues, when fetching the archlinux-keyring in the chroot
- Mirrors Ranking: Rank only Tier 1 Mirror's at installation time
- pacman.conf: Remove not used pacman repository
- cachy-chroot: Do not show .snapshot subvolumes
- Calamares: Do not use "Preservefiles" module, since user a reporting issues with it.

**Changelog for Handheld Edition:**
- Added configuration file to apply different scaling, '/home/$USER/.config/deckscale
- Make GameMode switching more robust
- Updated Wifi/Bluetooth Firmware for Steam Deck
- Implemented Auto Mount for GameMode
- Added gamescope-session quirks for Wine CPU Topology, HDR, and Backlight
- Fixed Refresh Rate Selection
- Updated jupiter-hw-support, steamdeck-dsp, jupiter-fan-control, gamescope-session-git

24.06
----

**Features:**
- chwd: Introduce handheld hardware detection
- chwd: Introduce T2 MacBook support
- chwd: Add network driver detection
- Installation: Added MacBook T2 support
- ISO: Add cachy-chroot. This is a script that helps the user to chroot into the system.
- ISO: Switch to Microcode Hooks; this requires using the latest Ventoy release (1.0.98)
- ISO: Enable copytoram; this no longer needs to be disabled because we don't provide the offline installation anymore
- filesystem: BTRFS is now the default selected file system
- netinstall: Use ufw instead of firewalld
- Calamares: Update Branding Slides
- Slides: Updated for latest changes
- Package Updates: linux-cachyos 6.9.3, mesa 24.1.1, xwayland 24.1, NVIDIA 555.52.04, Plasma 6.0.5

**Bug Fixes:**
- Calamares: umount: Enable emergency again
- Qtile: Multimedia Controls are now working correctly
- NVIDIA: Enable required services and options for working sleep on Wayland
- netinstall: Remove b43-fwcutter from installation
- netinstall: Replace hyprland-git with hyprland
- netinstall: Drop linux-cachyos-lts from selection to avoid issues with missing modules
- Calamares: Shellprocess: Move mirror ranking before installing keyring

**Changelog from Experimental Handheld Release:**
- Default to KDE Vapor Theme (SteamOS Theme)
- Default file system: BTRFS
- Default kernel: linux-cachyos-deckify
- SDDM now uses Wayland
- Environment Flag for HHD to reduce latency
- Added Kernel Arguments to improve Game Mode Switching behavior
- The username can now be edited
- Hardware Detection configures and installs required packages depending on the device used
- Mallit Keyboard now uses Dark Mode
- Valve's Powerbuttond for proper sleeping
- Shortcuts can now be added to Steam
- Updated scx-scheds to latest git commit, providing the latest enhancements for the LAVD Scheduler
- Added automount to cachyos-handheld
- CachyOS can now perform Steam Deck BIOS updates on the Steam Deck

24.05
----

**Features:**
- Filesystems: Introduce Bcachefs as a filesystem option
- pacstrap: Add detection if Bcachefs is used and install corresponding Bcachefs-tools
- CachyOS-AI-SDK: Introduce new install option to provide a OOB NVIDIA SDK Setup
- CachyOS-Deckify: Provide variant for Handhelds (experimental), see [here](https://discuss.cachyos.org/t/information-experimental-cachyos-deckify/203) for more details
- BTRFS: Automatic Snapper for snapshots, can be installed from within the CachyOS hello app.
- ISO: Drop Offline Installer
- Package Updates: Python 3.12, gcc 14.1.1, mesa 24.0.6, xwayland 24.1rc2 , NVIDIA 550.78

**Bug-Fixes:**
- settings.conf: Move hardware detection before netinstall
- pacstrap: Use btrfs-assistant instead of btrfs-assistant-git
- plymouth: remove plymouth hook on zfs + encryption
- ISO: Add various config files for KDE, to avoid getting screen locking during installation
- services-systemd: Properly enable fstrim.timer
- umount: Disable emergency to avoid issues with the zfs installation
- shellprocess: Cleanup leftovers from the offline installation

24.04
----

**Features:**
- Plymouth: Use plymouth to provide a themed boot animation
- ISO: Switch back to X11 due to issues when setting the keyboard layout in calamares
- rEFInd: New partitioning layout (seperate /boot and /boot/efi)
- netinstall: KDE: Install xwaylandvideobridge by default
- netinstall: Use lightdm instead of ly for various Desktop Environments, due to a bug in ly
- systemd-boot: Use @saved for systemd-boot to allow it to remember the previously selected boot entry
- cachyos-keyring: Refactor cachyos-keyring package and provide a cachyos-trusted keyring
- ISO: Use ZSTD 19 Compression for the mkinitcpio image of the ISO
- Package Updates: xz 5.6.1-3, linux-cachyos 6.8.2, pacman 6.1.0-5, mesa 24.0.4, Plasma 6.0.3, nvidia 550.67 and cachyos-settings 39-2

**Bug-Fixes:**
- Autologin: Fixed the autologin option when used together with sddm
- xz: Provide a patched xz package
- libarchive: Mitigate commit from malicious xz actor
- cachyos-settings: udev-rule: don't set watermark_scale_factor to 125, since it siginificantly increases RAM usage
- calamares: pacman-keyring: Use simpler method to integrate the keyring into the installation

24.03.1
----

**Features:**
- netinstall: Remove extra kernels in the netinstall selection to avoid confusion by users. Other custom kernels can be installed via Kernel Manager
- Kernel Manager: NVIDIA Modules are automatically installed when detected, Rebased for QT6, Fixed custom names when using LTO Option
- Package Installer: Rebased on QT6, updated for pacman 6.1
- Package Updates: linux-cachyos 6.8.1, pacman 6.1, mesa 24.0.3, Plasma 6.0.2, llvm 17.0.6

**Bug-Fixes:**
- NVIDIA: patched nvidia module to take the owner ship of nvidia.drm.modeset earlier to avoid issues on nvidia graphics
- Refind: Don't install the lts kernel to avoid issues
- shellprocess: Remove the liveusers directory completly

24.03
----

**Features:**
- ISO: Plasma 6 is now shipped in the ISO and uses Wayland as default, GNOME ISO got dropped to avoid confusion about netinstall
- Calamares: Rebased for QT6
- refind: Add f2fs and zfs as option including luks2 encryption
- mirrors: We provide now 2 global CDNs. One hosted by Cloudflare R2 and one hosted by Digital Ocean
- mirrorlist: Fetch the online installer directly from cdn to provide a faster delivery
- initcpiocfg: Use the new microcode hook for early loading the ucode
- bootloader: Dont load the microcode with the bootloader anymore
- Package Updates: linux-cachyos 6.7.9, mesa 24.0.2, zfs-utils 2.2.3

**Bug-Fixes:**
- pacstrap: Do not install config packages to provide the user a more clean selection of the installation
- shellprocess_pacman: Also copy the ranked cachyos-v4-mirrorlists to the target

24.02
-----

**Features:**
- refind: Change layout from /boot/efi to /boot to provide more options of filesystems and encryption
- Live-ISO: Cleanup and Sync the Live-ISO
- Launch Installer: Add recommendation for the online installation
- shell-configs: Add option to disable fastfetch when starting the terminal and add an "update" alias
- netinstall: Add phonon-qt5-vlc to kde
- Package Updates: linux-cachyos 6.7.5, mesa 23.3.5, gcc 13.2.1-12, glibc 2.39, mesa 24.0.1, nvidia 550.54.14

24.01
-----

**Features:**
- x86-64-v4: Autodetection and enabling the repository at installation
- linux-cachyos: the sched-ext scheduler framework is now provided in the default kernel
- xwayland: Provide explicit sync patches as default
- Package Updates: linux-cachyos 6.7, mesa 23.3.3, gcc 13.2.1-8, xorg-xwayland 23.2.4

**Bug Fixes:**
- chwd: For Ada Lovelace Nvidia cards the nvidia modules get directly packed into the initramfs to avoid issues with the early kms

23.12
-----

**Bug-fixes:**
- zfs: Add compatibility=grub to the pool options to ensure the compatibility
- grub/xfs: Add a patch to grub to have compatibility with the new xfs bigtime default
- netinstall: xdg-desktop-portal-hyprland instead of xdg-desktop-portal-hyprland-git

23.11
-----

**Features:**
- nvidia: Use nvidia module instead of dkms
- Calamares synced with upstream
- Package updates: linux-cachyos 6.6.1, nvidia-utils 545.29.02, mesa 23.2.1, zfs-utils 2.2.0, mkinitcpio 37

**Bug-fixes:**
- nvidia-hook: Added nvidia-hook back to avoid issues at installation time with the new module
- netinstall: Packages got renamed due the recent changes at the KF5 packaging
- netinstall: xdg-desktop-portal-gnome got added to the GNOME Installation

23.09
-----

**Features:**
- systemd-boot: Default to luks2
- netinstall: Provide a own category for CachyOS Packages
- Calamares synced with upstream
- Package updates: linux-cachyos 6.5.3, nvidia-utils 535.104.05, mesa 23.2.7

**Bug-fixes:**
- shellprocess_sdboot: Avoid using "sudo", when generating the boot entries at the installation process

23.08
-----

**Features:**
- Calamares synced with upstream
- Package updates: linux-cachyos 6.4.10, nvidia-utils 535.98

**Bug-fixes:**
- Keyring got updated and works now correctly


23.07
-----

**Features:**
- CachyOS-Settings includes now "bpftune", which automatically tweaks the network settings depending on the usage
- CachyOS-Qtile-Settings: Quality of Life changes, better icons, ...
- Package updates: linux-cachyos 6.4.2, cachy-browser 115.0.1, mesa 23.1.3,

**Bug-fixes:**
- rate-mirrors got fixed
- chwd (Hardware Detection) got multiple fixes
- fixed installation of nonfree drivers for hybrid setup in the installer
- fixed Calamares freezes, which happened in some rare configurations, mainly VM
- Slides: Slide 6 typo fix

23.06
-----

**Bug-fixes:**
- Offline Installation: Fix calamares

23.05
-----

**Features:**
- CachyOS Git Migration layout is now reflected in the installation
- chwd (mhwd) got multiple fixes
- Pacman: We added a feature, which makes it possible to provide a message to our users before updating
- Calamares got synced with upstream
- Package updates: linux-cachyos 6.3.4, cachy-browser 113.0.1, mesa 23.1.1, python 3.11

**Bug-fixes:**
- netinstall: minimal fixes due package changes
- Slides: Slide 6 got updated to reflect the lastest chang

23.04
-----

**Features:**

- Introduce the Qtile desktop enviroment
- Reworked mhwd: Rust rewrite; Simplified profiles for GPUs and network cards; Removed bunch of ancient code
- Package updates: linux-cachyos 6.2.12, cachy-browser 112.0.1, mesa 23.0.3, zfs-utils 2.1.11

**Bug-fixes:**

- f2fs: Remove "atgc" mount options since it has issues with systemd

23.03.1
-------

**Features:**

- Package updates: linux-cachyos 6.2.7, cachy-browser 111.0

**Bug-fixes:**

- Calamares got fixed with the lightdm displaymanager due faulty calamares upstream commits
- Offline installation keyring issue got fixed
- Refind: Use linux-cachyos-lts as defaullt. Current 6.2 seems not to work well together with refind


23.03
-----

**New Features:**

- Added the refind bootloader
- Automatic Nvidia driver installation using MHWD
- Encryption support for ZFS installation
- Added Hyprland to netinstallation
- CachyOS-KDE-Settings now uses the KDE default theme, but the CachyOS Themes are still preinstalled and available for use
- Package updates: linux-cachyos 6.2.2, mesa 23.0.0, cachy-browser 110.0.1, plasma 5.27.2
- Fully reworked and improved the bootloader calamares module
- The ISO gets now signed with a GPG key
- MHWD got improved and updated
- Synced Calamares with upstream

**Bug-fixes:**

- The "replace partition" option now offers a filesystem selection
- Fixed a typo in slide 3
- nouveau got fixed and does now proper load the module
- MHWD: Use modesetting for INTEL/ATI and Nouveau
- Removed the zfs hook from mkinitcpio on the live iso, which caused issues when booting
- You can download the update from our mirrors on SourceForge.

23.02
-----

**New Features:**

- The cachyos-community-v3 repo has been added
- Budgie, Mate, and LXDE desktop environments have been added to the Netinstallation
- Bluetooth.service is now enabled by default
- F2FS and grub are enabled and working again
- Package Updates: linux-cachyos 6.1.10, mesa 22.3.4, zfs-utils 2.1.9, glibc 2.37, cachy-browser 109.0.1

**Bug-fixes:**

- Rate-mirrors now fall back to unranked mirrors if it fails to rate them
- cachyos-rate-mirrors has a longer fetch-mirrors-timeout
- Github has been added to the hosts to avoid mirrorlist issues
- Boot entries for BIOS have been updated in syslinux


23.01
-----

**Features:**

- Calamares Slides got reworked and updated
- UKUI Desktop Enviroment got added to the Netinstallation
- Cinnamon Desktop Enviroment got added to the Netinstallation
- Cmdline: zswap is now disabled as default because CachyOS provides zram as default
- Calamares updated to the latest commit
- LLVM 15 is now shipped as default
- Package Updates: linux-cachyos 6.1.7, mesa 22.3.3, Plasma 5.26.5, llvm 15.0.7, gcc 12.1.1, binutils 2.40, zfs-utils 2.1.8, nvidia 525.85.05
- CLI Installer got updated

**Bug-fixes:**

- remove-ucode shellprocess does also run now at the offline installation
- pamac got removed from the netinstall
- The ranked cachyos mirrors gets now correctly copied to the install target
- power-profile-daemon don't gets enabled anymore as default


22.12
-----

**Features:**

- New GRUB background at the ISO bootloader
- memtest is now included for UEFI Systems
- CachyOS-sddm-theme got added to the KDE Installation
- Automatic version script added when creating the ISO
- Calamares updated to the latest commit
- The mirrors are now ranked with "cachyos-rate-mirros", which ranks our mirrors and the arch ones
- Packages Update: 6.1.1 Kernel, mesa 22.3.1, plasma 5.26.4,...
- The Kofuku Desktop Enviroment got removed
- extra ISO with llvm 15 included to provide support for newer AMD Cards


**Bug-fixes:**

- Calamares got fixed when using GNOME as ISO
- zfshostid does now work proper for the offline and online installation
- Add "kms" hook to the initcpiocfg module to follow archlinux defaults
- And more ISO fixes


22.11
-----

**Features:**

- Calamares and its config are shipped in one package
- Complete Cleanup of the packages in the netinstall
- Add a module which automatically removes the not needed ucode
- required RAM decreased to 2.5GB
- Packages which are required for btrfs, are now only installed for btrfs
- Calamares updated to the latest commit
- The ISO Bootloader has now a background
- Common package upgrades (mesa, kernel, ...)
- Replace systemd-network with networkmanager


**Bug-fixes:**

- qemu-quest-agent.service got removed from the ISO
- copytoram got completly disabled, it breaks the offline installation
- mkinitcpio.conf got updated
- And more ISO fixes


22.10
-----

**Features:**

- Pacman uses now Architecture=auto for x86-64-v3 installation, since we added a patch that pacman does autodetect x86-64-v3
- Pacman does show now, from which repo a package was installed
- Bootloader selection auto detect if EFI is present, if not it will default to grub
- Swap choice has been disabled now as default, since zram gets automatically dynamically generated
- Calamares updated to the latest commit
- Minimum RAM requirement has been set to 4GB
- cachyos-grub-theme got removed

**Bug-fixes:**

- SSD and hdd fstab detection has been disabled until there is a upstream fix
- double BTRFS subvolume has been fixed
- Added missing microcode to the ISO grub bootloader
- Added a fallback bootmode, which does not set any modeset (nomodeset)
- And more ISO fixes


22.09
-----

**Features:**

- Calamares is now on the latest 3.3 branch. Its brings bugfixes and new features to calamares
- TUI-Installer is now included in the GUI ISO, you can use it with "cachyos-installer"
- Calamares does now auto detect, if the target filesystem is a ssd or hdd and adjust to it the fstab options
- Nvidia for latest gpu's (starting at 9xx) has now a own boot entry, to avoid issues with nouveau
- fstab and zfs mount options got updated
- FireFox won't be installed as default anymore since cachy-browser is installed as default

**Bug-fixes:**

- cachyos-gaming-meta has been removed from the netinstall module to avoid issues at the installation process
- netinstall packages has been updated and got some fixes
- OpenBox installation has been fixed
- usual translation fixes


22.07
-----

**Features:**

- Boot-loader selection: User can now choose on the online installation between grub and systemd-boot
- At online installation will now always the newest calamares installed, which helps to do bug fixes on the "air"
- Calamares has now a mhwd module which automatically installs the needed drivers (free drivers)
- Calamares has new picture slides at the installation
- fstab and zfs mount options got updated
- HiDPI support

**Bug-fixes:**

- The locales bug in calamares got fixed
- F2FS has been removed for the grub boot loader since it is currently not working (calamares issue), it can be still with systemd-boot used
- Calamares shows now the correct default filesystem
- Gnome ISO got fixed
- Missing packages at the live ISO has been added for the offline installation
- btrfs swap luksencryption got fixed
- usual translation fixes

22.06
-----

Following known bugs has been fixed:

- Install failed when a generic CPU was used
- KDE did automatically mount zfs paritions which resulted that the auto login into the ISO did not worked anymore

**Improvements:**

- The firewall from the server has been corrected, cloudflare did blocked users as "bots", which resulted then into a error at installing
- Added theming support for Gnome, XFCE, OpenBox
- Updated our wiki

**_CachyOS - Kernel - Manager_**
Also we are excited to announce our CachyOS-Kernel-Manager.
Their you have the possibility to install the kernel from the repo and also configure with a GUI your own kernel build which makes is very easy to customize it to his own suits.

Following options you can select for a kernel compile:

- Scheduler (BMQ, BORE, cacULE, cfs, PDS, TT)
- NUMA disabled or enabled
- KBUILD CFLAGS (-O3 or -O2)
- Set performance governor as default
- Enable BBR2
- Tickrate (500Hz, 600Hz, 750Hz, 1000Hz)
- tickless (idle, perodic, full)
- disable MQ-Deadline I/O Scheduler
- disable Kyber I/O Scheduler
- Enable or disable MG-LRU
- Enable or disable DAMON
- Enable or disable Speculative page fault
- Enable or disable LRNG (Linux Random Number Generator)
- Apply Kernel automatic Optimization (Does automatically detect your CPU March)
- Apply Kernel Optimization slecting (You will see a list of different CPU-Marches and can select with a number yours)
- Disable debug (it lowers the size of the kernel)
- Enable or disable nf cone
- Enable LTO (Full, Thin, No)


22.05
-----

CachyOS was founded a year ago. After almost one year of development, we are really proud to announce our first Stable Release of GUI Installer.
We spent a lot of time investigating repo management, kernel development, infrastructure, theming, ... and finally put them all into the CachyOS GUI Installer.
All the features we worked on and implemented into the Installer are just trying to offer users a completely customizable experience.

The most exciting changes are that we use now for the online install pacstrap which provide then a complete clear installed environment and we do support a complete native support for the zfs filesystem

Since Discord restrict the length of the messages the full announcement can be found here:

https://discuss.cachyos.org/t/cachyos-gui-installer-changelog/

Download can be found here:
https://mirror.cachyos.org/ISO/kde/220522/
https://sourceforge.net/projects/cachyos-arch/
