---
title: Configuración de Hyprland
description: Atajos de teclado y FAQ de CachyOS Hyprland
---

:::caution
Dado que Hyprland comenzó su rediseño, ten en cuenta que actualmente no es estable y puedes experimentar errores/cierres inesperados. Úsalo bajo tu propia responsabilidad.
Incluso su versión "estable" también tiene fallos y errores, por lo que no planeamos proporcionar soporte más allá de nuestros archivos de configuración. Consulta su [wiki](<https://wiki.hyprland.org/>) en su lugar.
:::

:::tip
Inicia Hyprland utilizando la entrada sin systemd, de lo contrario no arrancará y te llevará a una pantalla negra.

Ejemplo: **`Hyprland`** en lugar de **`Hyprland(systemd)`**.
:::

Nuestro objetivo principal con nuestra configuración es tener un Hyprland funcional pero manteniéndolo simple, por lo tanto, pueden faltar algunas herramientas y programas esenciales como un Gestor de Archivos con interfaz gráfica.

Echa un vistazo a nuestras [FAQ de Hyprland.](/desktop_environments/hyprland#faq)

**Archivos de configuración mantenidos por [msmafra](https://github.com/msmafra) y [Lysec](https://github.com/Ly-sec)**

## Atajos de teclado

La mayoría de las combinaciones de teclas requieren el uso de la tecla mod, que en nuestro caso es la tecla Windows (referenciada como SUPER), puedes cambiarla en el archivo de configuración.

### Abrir terminal

* SUPER + Return

### Ir al espacio de trabajo (1-9)

* SUPER + 1-9 (Fila de números, el teclado numérico no cuenta)

### Cambiar enfoque a (Izquierda, Derecha, Arriba, Abajo)

* SUPER + Teclas de flecha

### Moverse entre espacios de trabajo con la rueda del ratón

* Super + Desplazamiento

### Moverse entre espacios de trabajo con coma y punto

* Super + punto (Siguiente espacio de trabajo)
* Super + coma (Espacio de trabajo anterior)

### Mover ventana enfocada al espacio de trabajo (1-9) sin ir allí

* SUPER + Shift + 1-9

### Lo mismo que arriba pero también cambiar a dicho espacio de trabajo

* SUPER + CTRL + 1-9

### Abrir Rofi (Lanzador de programas)

* SUPER + Espacio
  
### Cerrar ventana enfocada

* SUPER + Q

### Mover ventana enfocada en la dirección (Arriba, Abajo, Izquierda, Derecha)

* SUPER + Shift + Teclas de flecha

### Redimensionar ventana enfocada

* SUPER + CTRL + Shift + J (Hacia abajo)
* SUPER + CTRL + Shift + K (Hacia arriba)
* SUPER + CTRL + Shift + H (Izquierda)
* SUPER + CTRL + Shift + L (Derecha)
* SUPER + CTRL + Shift + Tecla de flecha (Cualquier dirección)

### Alternar ventana enfocada entre estado Flotante o Pantalla completa

* SUPER + F (Pantalla completa)
* SUPER + V (Flotante)

### Entrar en estado de submapa de redimensionamiento (Permite redimensionar), H,J,K,L o mediante teclas de flecha

* SUPER + R
* ESC para salir

### Mover ventana arrastrando el ratón

* SUPER + Clic izquierdo

### Redimensionar ventana

* SUPER + Clic derecho (mantenerlo presionado y arrastrar el cursor en cualquier dirección)

### Control de volumen (teclas multimedia) como SubirVol, BajarVol y SILENCIAR

### El control de brillo debería funcionar dependiendo del hardware

### Control de reproducción para pausar, reproducir, siguiente y anterior a través de teclas multimedia (Portátil o teclado)

### Fijar ventana enfocada para que se muestre en todos los espacios de trabajo (Flotante)

* SUPER + Y

### Alternar la ventana actual a un grupo

* SUPER + K

### Cambiar grupo activo

* SUPER + TAB

### Recargar Waybar

* SUPER + O

### Reducir espacio entre ventanas

* SUPER + G

### Restablecer espacios al valor predeterminado

* SUPER + Shift + G

### Abrir gestor de archivos (Variable no configurada por defecto)

* SUPER + E

### Captura de pantalla

* Impr Pant (PrtSc)

## FAQ

### ¿Por qué mi Discord, Thunar y Nautilus tienen un fondo extraño?

Esto se debe a que la ventana tiene una opacidad modificada

* Considera modificar la regla de ventana en el archivo de configuración de [Hyprland](https://github.com/CachyOS/cachyos-hyprland-settings/blob/master/etc/skel/.config/hypr/config/windowrules.conf#L21).

```sh title='Ejemplo'
windowrulev2 = opacity 0.92, class:^(thunar|nemo)$
```

### ¿Hay algún Gestor de Archivos incluido?

* No, instala el que prefieras
