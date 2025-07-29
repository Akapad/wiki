---
title: Kernel de CachyOS
description: Características y cambios en el kernel de CachyOS
---

El Kernel de CachyOS es un kernel personalizado que utiliza mejoras, configuraciones y parches procedentes de upstream.

## Características

- Elige entre 3 planificadores de kernel y varios planificadores [sched-ext](/configuration/sched-ext) para mejorar la capacidad de respuesta
- Mejoras de AMD P-State
- Último BBRv3 de Google
- le9uo para una capacidad de respuesta significativamente mejorada durante alta carga de memoria
- Conjunto de parches NTSYNC actualizado, usado con una versión compatible de wine/proton
- Compatibilidad con dispositivos MacOS T2 con parches de [t2linux](https://github.com/t2linux/linux-t2-patches/)
- Permite leer el uso de energía por núcleo para usuarios de AMD
- ACS Override y v412loopback
- Módulo VHBA para emular dispositivos CD/DVD-ROM
- Último conjunto de parches ZSTD
- Varios parches adicionales enfocados en mejorar el rendimiento (flags de compilador optimizadas, mejoras criptográficas, ajustes de gestión de memoria)

Para una lista más completa de los parches que ofrece CachyOS, consulta la 
[lista de características](https://github.com/CachyOS/linux-cachyos/?tab=readme-ov-file#features), el [repositorio kernel-patches](https://github.com/CachyOS/kernel-patches)
y el [Árbol de Fuentes Linux de CachyOS](https://github.com/CachyOS/linux).

## Variantes

CachyOS ofrece una amplia gama de opciones de kernel. Todos los kernels que proporcionamos se envían con el [Conjunto de Parches Base de CachyOS](https://github.com/CachyOS/kernel-patches).
Para cada uno de los kernels, existe una [variante `-lto` correspondiente](#convencion-de-nomenclatura-de-paquetes) que
se compila con [clang](https://clang.llvm.org/) en lugar de [GCC](https://gcc.gnu.org/). Tanto el kernel predeterminado como el `-rc` son excepciones a esto porque están
compilados con [ThinLTO](https://blog.llvm.org/2016/06/thinlto-scalable-and-incremental-lto.html) por defecto y por lo tanto tienen variantes de kernel `-gcc` correspondientes en su lugar.

- **linux-cachyos**
    - Frecuencia de tick de 1000Hz para mejorar la capacidad de respuesta.
    - Kernel predeterminado. Este es el kernel recomendado si no estás seguro sobre qué kernel deberías usar.
    - Utiliza el planificador [BORE](https://github.com/firelzrd/bore-scheduler).
    - Compilado con clang y ThinLTO por defecto para producir binarios más optimizados.
    - Perfilado con nuestro propio perfil [AutoFDO](https://cachyos.org/blog/2411-kernel-autofdo/) para mejorar el rendimiento. [Script](https://github.com/CachyOS/cachyos-benchmarker/blob/master/kernel-autofdo.sh) utilizado para perfilar el kernel.
- **linux-cachyos-bore**
    - Utiliza el planificador BORE.
- **linux-cachyos-bmq**
    - Utiliza el planificador BMQ del [Proyecto C](https://gitlab.com/alfredchen/projectc/) de Alfred Chen.
        - **No soporta sched-ext**.
- **linux-cachyos-deckify**
    - Kernel predeterminado para dispositivos portátiles. **No se recomienda** y **no está soportado** usar cualquier otro kernel en dispositivos portátiles que no sea este.
    - Utiliza el planificador BORE.
    - Parches específicos para dispositivos portátiles sobre el conjunto de parches base para mejorar la compatibilidad y la experiencia general en dispositivos portátiles.
- **linux-cachyos-eevdf**
    - Ajusta el planificador de kernel predeterminado para mejorar la capacidad de respuesta.
- **linux-cachyos-lts**
    - Basado en el último kernel con Soporte a Largo Plazo.
    - Utiliza el planificador BORE.
    - Mínimamente parcheado en comparación con otros kernels para garantizar la máxima estabilidad.
- **linux-cachyos-hardened**
    - Utiliza el planificador BORE.
    - Incluye el conjunto de parches [linux-hardened](https://github.com/anthraxx/linux-hardened).
    - Configuración del kernel basada en la [configuración de linux-hardened](https://gitlab.archlinux.org/archlinux/packaging/packages/linux-hardened/-/blob/main/config).
        - Contiene un endurecimiento muy agresivo que reduce significativamente el rendimiento y la experiencia del usuario.
        - **No soporta sched-ext**.
- **linux-cachyos-rc**
    - Basado en el último kernel principal del [árbol de Linus](https://github.com/torvalds/linux/).
    - Utiliza el planificador BORE.
    - Kernel principal para introducir nuevas características en nuestro conjunto de parches.
- **linux-cachyos-server**
    - Optimizado para cargas de trabajo de servidor en comparación con el uso de escritorio.
        - Frecuencia de tick de 300Hz.
        - Sin preemption.
        - EEVDF estándar.
- **linux-cachyos-rt-bore**
    - Preempción en tiempo real.
    - Utiliza el planificador BORE.

:::note
A menos que se especifique lo contrario, es seguro asumir que todas las demás variantes de kernel
tienen la misma configuración que el kernel predeterminado.
:::

Por favor, abre una incidencia en [GitHub de linux-cachyos](https://github.com/CachyOS/linux-cachyos) para sugerencias y mejoras que puedan añadirse al kernel predeterminado.

## Módulos de Kernel Precompilados

Para acomodar a una base de usuarios más amplia, CachyOS incluye algunos módulos de kernel bien conocidos y muy utilizados junto con el kernel. Esto significa que los usuarios ya no
tendrán que recompilar esos módulos después de cada actualización del kernel o en cada nueva instalación del kernel, sino que solo tendrán que instalarlos desde el repositorio ya que
están precompilados. Esto efectivamente hace obsoletos cualquier paquete `-dkms` que un usuario pueda tener que proporciona el mismo módulo que la versión precompilada.

### ZFS

[ZFS](https://openzfs.org/wiki/Main_Page) es uno de los muchos sistemas de archivos soportados en CachyOS. Debido a que está licenciado bajo
[CDDL](https://opensource.org/license/cddl-1-0), es incompatible con la licencia del kernel de Linux y por lo tanto no puede fusionarse en el árbol. El módulo incluido contiene
las últimas características y correcciones upstream para garantizar la compatibilidad con el kernel más reciente.

### NVIDIA

CachyOS incluye versiones precompiladas tanto del módulo de kernel de código cerrado como del [código abierto](https://github.com/NVIDIA/open-gpu-kernel-modules/). Debido a que el desarrollo
del módulo de NVIDIA es fuera del árbol y, por lo tanto, no sigue el ritmo de lanzamiento del kernel, la configuración estándar a veces puede ser incompatible con el último
kernel. Como solución, CachyOS parcela los módulos con parches creados por la comunidad o parches compartidos directamente por NVIDIA.

## Otros

El kernel de CachyOS también tiene algunas otras características notables que son sutiles pero mejoran la experiencia del usuario

- Incluye una variante de depuración del kernel que proporciona un binario de kernel no reducido para fines de depuración. Este paquete es necesario para perfilar el kernel con AutoFDO.
- [Binder](https://developer.android.com/reference/android/os/Binder), el módulo necesario para [Waydroid](https://waydro.id/) está habilitado por defecto en la configuración del kernel
y ya está [configurado](https://github.com/CachyOS/linux-cachyos/blob/master/linux-cachyos/config#L10559).

## Convención de Nomenclatura de Paquetes

```sh
linux-cachyos # Paquete de kernel base para el kernel predeterminado. Compilado con clang
linux-cachyos-gcc # Contraparte compilada con GCC para linux-cachyos
linux-cachyos-{,gcc-}headers # Cabeceras del kernel, principalmente para compilar
linux-cachyos-{,gcc-}nvidia # Módulos NVIDIA de código cerrado precompilados para el kernel linux-cachyos
linux-cachyos-{,gcc-}nvidia-open
linux-cachyos-{,gcc-}zfs # Módulos ZFS precompilados para el kernel linux-cachyos
linux-cachyos-{,gcc-}dbg # Binario linux no reducido para depuración

linux-cachyos-hardened # Paquete de kernel base para el kernel endurecido. Compilado con GCC
linux-cachyos-hardened-lto # Contraparte compilada con clang para linux-cachyos-hardened
linux-cachyos-hardened-{,lto-}headers
linux-cachyos-hardened-{,lto-}nvidia
linux-cachyos-hardened-{,lto-}nvidia-open
linux-cachyos-hardened-{,lto-}zfs
linux-cachyos-hardened-{,lto-}dbg
```

## Preguntas Frecuentes

### ¿Por qué no se utiliza AutoFDO para todas las demás variantes de kernel?

Porque es costoso de construir ya que básicamente requiere compilar el kernel dos veces, por lo tanto requiere más recursos y tiempo dedicados a la compilación. El proceso de construir un kernel con AutoFDO implica los siguientes pasos:

1) Construir el kernel con capacidades de AutoFDO y depuración habilitadas.
2) Crear un perfil, lo que significa ejecutar cargas de trabajo para recopilar datos de perfilado para las posibles optimizaciones.
3) Reconstruir el kernel con el perfil AutoFDO.

Por lo tanto, por ahora solo está presente en la variante [linux-cachyos](/features/kernel#variants).

Para más información sobre AutoFDO, haz clic [aquí.](https://cachyos.org/blog/2411-kernel-autofdo/)

### ¿El kernel de tiempo real mejora el rendimiento en juegos?

No, no lo hace. El kernel de tiempo real hace que mucho más código sea preemptible en comparación con un kernel normal completamente preemptible. Esto significa que muchas más tareas (incluidos los procesos de juegos)
son frecuentemente preemptadas y cederán forzosamente los recursos del sistema, lo que lleva a un peor rendimiento.
