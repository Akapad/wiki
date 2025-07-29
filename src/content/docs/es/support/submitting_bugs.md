---
title: Envío de errores
---

# Describe tu problema

- *¿Qué no está funcionando?*
- *¿Soluciona el problema la degradación del paquete X?*
- *Utiliza la función de búsqueda para encontrar problemas similares*
- *¿Has realizado modificaciones por tu cuenta?*
  - Ejemplo: `Añadir una bandera adicional en un archivo modprobe`

# Proporciona registros

CachyOS ofrece una excelente herramienta para recopilar registros del sistema llamada `cachyos-bugreport.sh`.
Esta herramienta recopilará registros de:
- dmesg
- journalctl
- inxi `(Para recopilar información del hardware)`

Cuando se recopilen los registros, se preguntará al usuario si desea subirlos a nuestro sitio web de pegado.

**Ejecuta el siguiente comando en la terminal y publica el enlace con los errores en el tema:**
```sh
sudo cachyos-bugreport.sh
```

# Enlaces para enviar informes

- Github: <https://github.com/CachyOS/distribution>
- Foro: <https://discuss.cachyos.org/c/feedback/bugreports/10>
- Discord: [Canal de soporte](https://discord.com/channels/862292009423470592/862294383470051348)
