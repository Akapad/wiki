---
title: Aceleración por Hardware en Navegadores Basados en Chromium
description: Configura la aceleración por hardware para decodificación/codificación de vídeo en navegadores basados en Chromium en CachyOS. Incluye configuración para GPUs AMD y una plantilla para otras GPUs/navegadores.
---

# Aceleración por Hardware en Navegadores Basados en Chromium

Esta guía detalla cómo habilitar la aceleración por hardware en navegadores basados en Chromium en CachyOS. Esto descarga las tareas de vídeo/gráficos a tu GPU, mejorando el rendimiento.

## Requisitos Previos

* **Navegador basado en Chromium:** (ej., Chrome, Brave, Ungoogled Chromium, Edge)
* **Controladores/APIs de GPU:** Mesa actualizado (AMD/Intel) o controladores NVIDIA, con Vulkan/VA-API/VDPAU configurados.
* **`amdgpu_top` (para usuarios AMD):** Instala `amdgpu_top` desde el repositorio mediante el gestor de paquetes si deseas monitorizar la actividad de la GPU AMD desde el terminal.

## Contribución

Esta guía es extensible. Si tienes una configuración de aceleración por hardware funcional para una GPU específica y un navegador basado en Chromium, contribuye añadiendo una nueva sección bajo "Configuraciones de GPU y Navegador". Incluye:

* **Nombre del Navegador**
* **Modelo de GPU**
* **Flags:** Contenido del archivo `~/.config/[navegador]-flags.conf`.
* **Ruta del Archivo:** Ruta completa al archivo de flags.
* **Notas (Opcional):** Controladores clave, paquetes o especificaciones de configuración.

## Pasos de Configuración

1.  **Identificar Archivo de Flags:** Localiza la ruta del archivo de flags de tu navegador en "Configuraciones de GPU y Navegador".
2.  **Editar Archivo de Flags:** Abre/crea el archivo usando `nano` (o tu editor de texto preferido como `micro`, `vim`).
    ```bash
    nano [RUTA_A_TU_ARCHIVO_DE_FLAGS]
    # Ejemplo: nano ~/.config/chrome-flags.conf
    ```
3.  **Añadir Flags:** Pega los flags relevantes de GPU/navegador en el archivo.
4.  **Guardar y Cerrar.**
5.  **Reiniciar Navegador:** Cierra todas las instancias del navegador y vuelve a lanzarlo.
6.  **Verificar:** Navega a `chrome://gpu` (o `brave://gpu`, `edge://gpu`, etc.). Confirma el estado "Acelerado por hardware" bajo "Información de Aceleración de Vídeo" y "Estado de Características Gráficas".

## Consejos de Verificación

Para comprobar definitivamente si la aceleración por hardware está activa durante la reproducción de vídeo, utiliza estos métodos:

### 1. Comprobar la Utilización de GPU AMD (`amdgpu_top`)

Si tienes una GPU AMD y `amdgpu_top` instalado, abre un terminal y ejecútalo:

```bash
amdgpu_top
````

Mientras se reproduce un vídeo en tu navegador (ej., YouTube), observa la sección `media` en `amdgpu_top`. Deberías ver alguna utilización aquí, indicando que el motor multimedia de tu GPU está activo. Si permanece al 0% durante la reproducción de vídeo, es posible que la aceleración por hardware no esté completamente activada para la decodificación.

### 2. Comprobar las Herramientas de Desarrollo del Navegador (Decodificador de Vídeo)

Este método proporciona confirmación directa desde el propio navegador:

1. Abre tu navegador basado en Chromium.
    
2. Comienza a reproducir un vídeo (ej., en YouTube o un archivo local).
    
3. Abre las Herramientas de Desarrollo: Pulsa `F12` o `Ctrl+Shift+I`.
    
4. Navega a la pestaña **Media**. Si no la ves, haz clic en los tres puntos (`...`) o `>>` (Más pestañas) en la barra de herramientas de Desarrollo, luego selecciona `Media`.
    
5. En la sección "Players" a la izquierda, haz clic en la entrada correspondiente a tu vídeo.
    
6. En el panel principal, desplázate hacia abajo hasta la sección **Video Decoder**.
    
7. Busca la etiqueta `Hardware decoder`. Debería ser `true`. Si dice `false` o muestra el nombre de un decodificador por software (ej., `FFmpegVideoDecoder`, `VpxVideoDecoder`, `Dav1dVideoDecoder`), la aceleración por hardware no está activa para ese vídeo.
    

## Configuraciones de GPU y Navegador

### AMD Radeon RX 6900 XT (Google Chrome)

- **Navegador:** Google Chrome
    
- **GPU:** AMD Radeon RX 6900 XT
    
- **Archivo de Flags:** `~/.config/chrome-flags.conf`
    

```bash
--use-gl=angle
--use-angle=vulkan
--enable-features=Vulkan,VulkanFromANGLE,DefaultANGLEVulkan,AcceleratedVideoDecodeLinuxZeroCopyGL,AcceleratedVideoEncoder,VaapiIgnoreDriverChecks,UseMultiPlaneFormatForHardwareVideo
--ozone-platform-hint=x11
```

**Notas:** Aprovecha Vulkan (vía ANGLE) y VA-API. `--ozone-platform-hint=x11` puede ser útil incluso en Wayland para ciertas rutas de aceleración.

---

### Plantilla para contribuir

### [Tu Navegador] - [Tu Modelo de GPU] (Contribuido por [Tu Nombre/Alias])

- **Navegador:** [ej., Brave, Ungoogled Chromium, Microsoft Edge, Vivaldi, Opera, Chromium]
    
- **GPU:** [ej., NVIDIA GeForce RTX 3080, Intel Iris Xe]
    
- **Ruta del Archivo de Flags:** (Crucial, ¡varía según el navegador!)
    
    - **Rutas comunes de `.conf`:**
        
        - **Chromium:** `~/.config/chromium-flags.conf`
            
        - **Brave Browser:** `~/.config/brave-browser-flags.conf`
            
        - **Ungoogled Chromium:** `~/.config/ungoogled-chromium-flags.conf`
            
    - **Modificación de archivo `.desktop`:** Algunos navegadores (Brave, Edge, Vivaldi, Opera) podrían requerir editar la línea `Exec=` en su archivo `.desktop` (copia primero desde `/usr/share/applications/` a `~/.local/share/applications/`).
        

**Contenido de Flags (para archivo `.conf` o línea `Exec=`):**

```bash
# Pega tus flags aquí.
# Para archivos .desktop, los flags se separan por espacios después del ejecutable.
```

**Notas (Opcional):**

- Controladores requeridos (ej., `nvidia-dkms`, `intel-media-driver`).
    
- Consideraciones específicas de configuración o instrucciones de modificación del archivo `.desktop`.
