---
title: ¿Por qué CachyOS?
description: Porque CachyOS puede ser mejor para ti
---

CachyOS ofrece una experiencia de Arch Linux pulida y completa con un instalador fácil de usar, escritorios pre-configurados y optimizaciones de rendimiento sin comprometer la experiencia del usuario y la seguridad del sistema.

A continuación se presentan algunas de las características principales que CachyOS proporciona para garantizar una experiencia de escritorio mejorada.

## Paquetes y Repositorios Optimizados

CachyOS ofrece una amplia selección de paquetes optimizados para diversas configuraciones de hardware, incluyendo sistemas `x86-64-v3`, `x86-64-v4` y `Zen4+` para mejorar el rendimiento general.

Para más información, consulta [**Repositorios Optimizados.**](/features/optimized_repos)

## Kernel Personalizado Optimizado para Rendimiento y Estabilidad

Además del conjunto base de parches del kernel de CachyOS que ajustan varios parámetros del kernel para mejorar la capacidad de respuesta del escritorio, CachyOS selecciona conjuntos de parches que no han sido incluidos en la rama principal o no están incluidos en la revisión estable del kernel.

Por lo tanto, estos parches se someten a pruebas internas antes de ser liberados a los usuarios para garantizar que la estabilidad no se vea afectada. Para una lista completa de los parches que proporciona CachyOS, consulta [Kernel](/features/kernel).

## Soporte de Planificadores de CPU Personalizados

Por defecto, EEVDF está configurado para dividir el tiempo de CPU disponible de manera equitativa entre todas las tareas y está principalmente orientado a cargas de trabajo centradas en el rendimiento. El kernel de CachyOS [**configura algunos parámetros ajustables de EEVDF**](https://github.com/CachyOS/linux/blob/6.15/cachy/kernel/sched/fair.c#L79-81) para priorizar la interactividad del escritorio.

Sin embargo, EEVDF por diseño no fue pensado para ser utilizado en la interactividad del escritorio. Teniendo esto en cuenta, CachyOS ofrece kernels parcheados con el planificador [BORE (Burst-Oriented Response Enhancer)](https://github.com/firelzrd/bore-scheduler) que mejora EEVDF para optimizar la interactividad bajo cargas de trabajo intensas.

En la versión 6.12, el kernel de Linux introdujo la capacidad de conectar planificadores BPF en caliente y reemplazar EEVDF por un planificador diferente.

Para más información sobre los kernels ofrecidos por CachyOS y los planificadores sched-ext, consulta [Kernel](/features/kernel) y [sched-ext](/configuration/sched-ext).

## Detección de Hardware

CachyOS incluye su propia herramienta de detección de hardware, que identifica automáticamente e instala los controladores y paquetes necesarios para cada sistema, simplificando el proceso posterior a la instalación para los usuarios.

## Proceso de Instalación Personalizable

El instalador de CachyOS permite a los usuarios personalizar su sistema eligiendo el entorno de escritorio, paquetes, sistema de archivos, gestor de arranque, kernel y más para adaptarse a sus necesidades:
- [**Entornos de Escritorio**](/installation/desktop_environments/)
- [**Gestores de Arranque**](/installation/boot_managers/)
- [**Variantes de Kernel**](/features/kernel#variants)
- [**Sistemas de Archivos**](/installation/filesystem)
- [**Paquetes personalizados para incluir durante la instalación**](https://github.com/CachyOS/cachyos-calamares/blob/cachyos-limine-qt6/src/modules/netinstall/netinstall.yaml)

## Aplicaciones de CachyOS

Por defecto, CachyOS proporciona su propio conjunto de aplicaciones, como CachyOS Hello y el Instalador de Paquetes de CachyOS.

Lista de aplicaciones que CachyOS actualmente desarrolla y mantiene:

- [**CachyOS Kernel Manager**](https://github.com/CachyOS/kernel-manager): Instala fácilmente kernels desde el repositorio o configura tu propio kernel e incluye tus propios parches e incluso gestiona el framework sched-ext a través del [**scx_loader**](<https://github.com/sched-ext/scx/tree/main/rust/scx_loader>).
- [**CachyOS Hello**](https://github.com/CachyOS/CachyOS-Welcome): Aplicación para controlar ajustes, aplicar correcciones, instalar paquetes y más información sobre CachyOS.
- [**CachyOS Package Installer**](https://github.com/CachyOS/packageinstaller): Interfaz gráfica para una fácil instalación de aplicaciones.
- [**cachyos-rate-mirrors**](https://github.com/CachyOS/rate-mirrors): Clasifica automáticamente los espejos de Arch y CachyOS para velocidades de descarga óptimas con pacman.
- [**systemd-boot-manager**](https://github.com/CachyOS/systemd-boot-manager): Genera automáticamente nuevas entradas para el gestor de arranque systemd-boot y puede configurarse fácilmente en `/etc/sdboot-manage.conf`.

## Comunidad Amigable y Activa

La mayor fortaleza de CachyOS es su comunidad en expansión. Sin su apoyo, CachyOS no habría alcanzado su éxito actual. Los miembros de la comunidad se ayudan mutuamente compartiendo consejos y trucos para mejorar la experiencia Linux.

Únete a nosotros en el [**Discord de CachyOS**](https://discord.com/invite/cachyos-862292009423470592) y en el [**Foro de CachyOS**](https://discuss.cachyos.org/).

