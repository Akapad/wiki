---
title: Configuración de Qtile
description: Atajos de teclado y preguntas frecuentes de CachyOS Qtile
---

Créditos a [Shendisx](<https://github.com/Shendisx>) por crear esta configuración de Qtile.

> Sesión X11 y Wayland

## Atajos de teclado

La mayoría de las combinaciones de teclas requieren el uso de la tecla mod que en nuestro caso es la tecla Windows (referenciada como SUPER), puedes cambiarla en el archivo de configuración.
Algunas de ellas podrían hacer uso de mod1 (tecla ALT).

### Abrir terminal

* SUPER + Return

### Cerrar ventana enfocada

* SUPER + Q

### Ir al espacio de trabajo (1-9)

* SUPER + 1-9 (Fila de números, el teclado numérico no cuenta)

### Abrir Rofi (Lanzador de programas)

* ALT + Espacio

### Mover el enfoque a (Izquierda, Derecha, Abajo, Arriba)

* SUPER + H (Izquierda)
* SUPER + L (Derecha)
* SUPER + J (Abajo)
* SUPER + K (Arriba)
* SUPER + Espacio (Mover ventanas entre columnas izquierda/derecha o mover arriba/abajo en la pila actual)

### Mover ventana enfocada a (Izquierda, Derecha, Abajo, Arriba)

* SUPER + Shift + H (Izquierda)
* SUPER + Shift + L (Derecha)
* SUPER + Shift + J (Abajo)
* SUPER + Shift + K (Arriba)

### Aumentar ventana enfocada hacia (Izquierda, Derecha, Abajo, Arriba)

* SUPER + Control + H (Izquierda)
* SUPER + Control + L (Derecha)
* SUPER + Control + J (Abajo)
* SUPER + Control + K (Arriba)

### Restablecer todos los tamaños de ventana del espacio de trabajo actual a su tamaño original

* SUPER + N

### Alternar pantalla completa en ventana enfocada

* SUPER + F

### Alternar flotante en ventana enfocada

* SUPER + V

### Alternar entre lados divididos y no divididos de la pila

* SUPER + Shift + Return

### Alternar entre diseños

* SUPER + TAB

### Recargar archivo de configuración de Qtile

* SUPER + Control + R

### Salir de Qtile (finalizar sesión X en ejecución)

* SUPER + Control + Q

### Ejecutar Flameshot (Utilidad para tomar capturas de pantalla)

* Print

### Capturar una captura de pantalla completa (Guardada en $HOME/Pictures)

* Control + Print

### Abrir Gestor de Archivos (Thunar por defecto)

* SUPER + E

### Arrastrar una ventana flotante con el ratón

* SUPER + Clic Izquierdo

### Aumentar una ventana flotante con el ratón

* SUPER + Clic Derecho

### Traer ventana al frente

* SUPER + Botón de la rueda de desplazamiento

### Fijar ventana (Por ejemplo, fijar Firefox PIP ahora te seguirá entre espacios de trabajo)

* SUPER + S

## Preguntas frecuentes

### ¿Por qué el widget de volumen muestra un error o está atascado en 0%?

* A veces esto se debe a que el widget de volumen de Qtile no puede detectar tu dispositivo de salida predeterminado, puedes consultar la wiki para más información.
* <https://docs.qtile.org/en/latest/manual/ref/widgets.html#pulsevolume>

### ¿Hay un script autostart.sh?

* Está ubicado en scripts/ desde la carpeta de Qtile

### ¿La barra de Qtile interactúa con el ratón?

* Sí lo hace, por ejemplo, si desplazas sobre los pequeños puntos que son tus espacios de trabajo (Activo, Inactivo, Vacío, etc.) cambiarás a la Izquierda o Derecha o incluso puedes hacer clic en uno de ellos.
* Otro ejemplo es el diseño (columnas por defecto), haciendo clic en él te permite cambiar entre los diseños disponibles
* Uso de CPU y RAM, al hacer clic abrirá Btop (Monitor del Sistema TUI)
* Aumentar/Bajar/Silenciar interactuando con el widget de volumen

Para más información sobre Qtile. Por favor, consulta su wiki como referencia.

* <https://docs.qtile.org/en/stable/>
