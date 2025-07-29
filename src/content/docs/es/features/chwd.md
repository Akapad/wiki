---
title: Detección de Hardware de CachyOS
description: Detección y Configuración de Hardware para CachyOS
---

[CachyOS Hardware Detection](https://github.com/CachyOS/chwd/) o más conocido como **`chwd`** nos permite utilizar diversos tipos de hardware instalando los paquetes
y controladores necesarios para el sistema en ejecución. Esto incluye sistemas con tarjetas gráficas NVIDIA, Macbooks T2 y dispositivos portátiles como Steam Deck y ROG Ally.

## Uso

**`chwd`** normalmente se ejecuta durante la instalación para proporcionar los paquetes necesarios para el sistema. Sin embargo, también es posible
usarlo después de la instalación.

### Configuración Automática

**`chwd`** permite instalar y configurar los controladores y paquetes necesarios para que el sistema funcione en condiciones óptimas.

```sh
❯ sudo chwd -a
```

### Instalación de un perfil

Una alternativa al método anterior es instalar cada perfil específico.

```sh title='Listar todos los perfiles disponibles'
❯ chwd --list-all
╭─────────────────────────┬─────────╮
│ Nombre                  ┆ NonFree │
╞═════════════════════════╪═════════╡
│ nvidia-open-dkms.prime  ┆ true    │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ nvidia-dkms             ┆ true    │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ macbook-t2              ┆ false   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ phoenix                 ┆ false   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ steam-deck              ┆ false   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ amd                     ┆ false   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ intel                   ┆ false   │
╰─────────────────────────┴─────────╯
```

```sh title='Instalar un perfil chwd'
❯ sudo chwd -i amd
> Instalando amd ...

> amd instalado correctamente
```

### Otros

Consulta la ayuda de **`chwd`** para conocer la sintaxis de los comandos y otros usos.

```sh
❯ chwd --help
Uso: chwd [OPCIONES]

Opciones:
  -i, --install <perfil>           Instalar perfil
  -r, --remove <perfil>            Eliminar perfil
  -d, --detail                     Mostrar información detallada en los listados
  -f, --force                      Forzar reinstalación
      --list-installed             Listar kernels instalados
      --list                       Listar perfiles disponibles para todos los dispositivos
      --list-all                   Listar todos los perfiles
  -a, --autoconfigure [<classid>]  Autoconfigurar
      --ai_sdk                     Alternar perfiles AI SDK
      --pmcachedir <PMCACHEDIR>    [predeterminado: /var/cache/pacman/pkg]
      --pmconfig <PMCONFIG>        [predeterminado: /etc/pacman.conf]
      --pmroot <PMROOT>            [predeterminado: /]
  -h, --help                       Mostrar ayuda
  -V, --version                    Mostrar versión
```
