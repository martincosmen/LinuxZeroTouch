# Arquitectura del Sistema

Este documento describe la arquitectura general del sistema automatizado de instalación y configuración de Linux.
Incluye una visión general de los componentes clave, como el servidor PXE, el proceso de instalación con Preseed, la configuración con Cloud-init y Ansible, y cómo se integran todas las partes para proporcionar una solución escalable y eficiente.

## Diseño de Red

La arquitectura de red propuesta se basa en un entorno local (LAN) donde un servidor central será el encargado de ofrecer servicios de arranque por red (PXE) y automatización de la instalación de sistemas operativos Linux.

Este servidor ejecutará los servicios necesarios para proporcionar imágenes del sistema, configuraciones personalizadas y automatizar los primeros pasos tras la instalación.

El diseño está pensado para un entorno de pruebas con máquinas virtuales, aunque es completamente aplicable a entornos físicos. Todos los clientes estarán conectados a la misma red local, y arrancarán a través de PXE para recibir automáticamente el sistema operativo y su configuración.

## Componentes de la Red

- **Servidor PXE**
- **Switch**
- **Equipos Linux (2)**

## Justificación del uso de Switch

La elección de un switch en lugar de un router se debe a:

- Mayor control sobre redes locales
- No es necesario que actúe como puerta de enlace a internet
- Mayor aislamiento del tráfico local (DHCP, TFTP, HTTP…)

Aunque el entorno planteado se basa en una red de pruebas, este diseño es perfectamente aplicable en entornos reales. En muchas empresas se utilizan switches para interconectar servidores y clientes dentro de redes locales, mientras los servicios necesarios (como DHCP, TFTP y HTTP) se ejecutan en uno o varios servidores.

Esta separación facilita el control, el mantenimiento y la escalabilidad del sistema.

## Diagrama lógico de red

![Diagrama de red](/docs/pics/diagrama_red.png)

## 4.2.1. Comunicaciones externas

En este proyecto no se establece ninguna conexión con redes externas ni con Internet. Todo el entorno está diseñado para funcionar de manera completamente local, dentro de una red LAN aislada.

El objetivo principal es simular un entorno de despliegue controlado, donde el servidor PXE proporciona todos los recursos necesarios (imágenes del sistema, configuraciones automatizadas, scripts, etc.) sin necesidad de acceder a repositorios online ni realizar descargas externas.

Este enfoque garantiza mayor control sobre el proceso, evita dependencias externas y permite realizar pruebas de manera segura y autónoma. Además, refleja el comportamiento habitual de muchas redes empresariales, donde la instalación de sistemas se realiza en entornos cerrados por motivos de seguridad.

En una implementación real, el servidor podría estar conectado a internet para obtener paquetes actualizados o acceder a repositorios. De todos modos, esta conexión se daría mediante una salida NAT que estaría totalmente controlada por el firewall corporativo de la empresa.
