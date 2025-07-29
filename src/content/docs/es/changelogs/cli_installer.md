---
title: Registro de cambios del instalador CLI de CachyOS
description: Registros de cambios del instalador CLI
---
# 0.8.4

## Características ✨

- **Gestión mejorada de particiones:** Se ha realizado una refactorización significativa y mejoras en cómo el instalador maneja las particiones, lo que lleva a una mayor precisión y fiabilidad.
- **Generación de parámetros del kernel:** El instalador ahora genera automáticamente parámetros del kernel basándose en el esquema de particiones detectado.
- **Biblioteca `gucc` mejorada:** La biblioteca `gucc` ha sido significativamente mejorada, ahora incluye capacidades de instalación y configuración de refind.

## Tareas de mantenimiento 🧹

- **Clang-Format y Clang-Tidy:** La consistencia y calidad del código se han mejorado mediante la aplicación de clang-format y clang-tidy.
- **Refactorización con String Views:** Varias áreas del código ahora utilizan literales string_view para mejorar el rendimiento y la legibilidad.
- **Implementación de Doctest:** Los asertos de C han sido reemplazados con doctest para pruebas más robustas e informativas.
- **Pruebas refactorizadas:** Los conjuntos de pruebas han sido refactorizados para mejorar la claridad y mantenibilidad.
- **Gestión de Refind en `gucc`:** El código relacionado con refind ha sido refactorizado y trasladado a la biblioteca `gucc` para una mejor organización y mantenibilidad.

## Corrección de errores 🐛

- **Detección de subvolúmenes Btrfs:** Se han resuelto problemas con la detección de subvolúmenes btrfs existentes.
- **Precisión de información de particiones:** Se han realizado mejoras para garantizar la recopilación y visualización precisa de información de particiones.
- **Punto de montaje raíz para Refind:** Se ha corregido un error que afectaba al punto de montaje raíz utilizado por refind.
- **Detección de UUID:** Se ha mejorado el proceso de detección de UUID de particiones durante la inicialización.
- **Correcciones en el proceso de compilación Meson:** Se han solucionado problemas encontrados durante el proceso de compilación con meson.
- **Anexión de subvolúmenes Btrfs:** Se ha corregido un error relacionado con la anexión de subvolúmenes btrfs en entornos de desarrollo.
- **Rootfs en configuraciones predefinidas:** Se ha resuelto un problema con el rootfs de esquemas de partición derivados de configuraciones predefinidas.
- **Montaje de lectura-escritura para Refind:** Se ha asegurado que refind monte las particiones necesarias con permisos de lectura-escritura.

# 0.8.3

## Tareas de mantenimiento 🧹

- Actualización de la dependencia CPR a una versión más reciente para mejorar la funcionalidad.
- Se instruyó explícitamente a CTRE (biblioteca de Expresiones Regulares en Tiempo de Compilación) para utilizar el estándar C++23 para consistencia y posibles mejoras de rendimiento.
- Se aumentó el tiempo de espera para la comprobación de conexión en la sección de utilidades para adaptarse a posibles retrasos de red o respuestas lentas.

# 0.8.2

## Correcciones 🐛

- Se resolvió un problema donde "gucc" no manejaba correctamente los puntos de montaje de subvolúmenes btrfs.
- Se mejoró "gucc" para manejar diferentes estados de montaje de subvolúmenes btrfs.

## Tareas de mantenimiento 🧹

- Se corrigió un error tipográfico en el archivo README y se actualizó la información de versión.

# 0.8.1

## Correcciones 🐛

- Se resolvió un problema donde los repositorios ISA se activaban incorrectamente en Oracle VM.
- Se abordaron inconsistencias de estilo en comandos para mejorar la experiencia del usuario.

## Tareas de mantenimiento 🧹

- Se eliminó la lógica innecesaria de ucode relacionada con refind, simplificando el código base.

# 0.8.0

## Características ✨

- Se añadió un analizador para perfiles de paquetes de red.
- Se introdujo la capacidad de obtener paquetes de entorno desde un archivo TOML analizado por gucc.
- Se implementó una función auxiliar en gucc para descargar archivos desde URLs 📥.
- Se añadió soporte para obtener perfiles de red desde una URL con un mecanismo de respaldo dentro de gucc.
- Se integró la instalación de perfiles de red con la distribución binaria.
- Se trasladó el montaje de particiones específicas y la lógica de detección a gucc.
- Se introdujo `utils::exec_checked` para una ejecución más segura de comandos externos.

## Mejoras ✅

- Se mejoró la cobertura de pruebas para la funcionalidad crypttab en gucc 🧪.
- Se mejoró el registro en gucc configurando el logger apropiadamente.
- **Actualización de la versión de C++ a C++23** ⬆️.
- Se refactorizó el código base para utilizar características de C++23 como `std::ranges` y `contains` para mejor legibilidad y eficiencia.
- Se refactorizaron varios componentes para utilizar `utils::exec_checked`.

## Correcciones 🐛

- Se resolvió un problema con tipos de biblioteca codificados en gucc.
- Se abordó la falta de implementación y archivo de cabecera del logger en gucc.
- Se habilitó la biblioteca CPR para compilaciones en entornos no de desarrollo.
- Se corrigió el proceso de compilación estática.
- Se abordaron problemas introducidos en el commit [`a70e641e364`](https://github.com/CachyOS/New-Cli-Installer/commit/a70e641e364).
- Se corrigieron errores de compilación en el componente TUI.
- Se corrigió un problema de dependencia donde la dependencia de FTXUI en range-v3 no era pública.

## Tareas de mantenimiento 🧹

- Se actualizaron las comprobaciones de CI, procesos de compilación, y se corrigieron problemas relacionados.
- Se eliminó la instalación revertida de perfiles de red junto con la distribución binaria.
- Se refactorizó y limpió el código en varios componentes: TUI, utils, chwd_profiles, user, y tests.
- Se eliminó la biblioteca range-v3 no utilizada de las dependencias del instalador.
- Se actualizó el archivo README.
