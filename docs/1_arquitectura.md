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

## Comunicaciones externas

En este proyecto no se establece ninguna conexión con redes externas ni con Internet. Todo el entorno está diseñado para funcionar de manera completamente local, dentro de una red LAN aislada.

El objetivo principal es simular un entorno de despliegue controlado, donde el servidor PXE proporciona todos los recursos necesarios (imágenes del sistema, configuraciones automatizadas, scripts, etc.) sin necesidad de acceder a repositorios online ni realizar descargas externas.

Este enfoque garantiza mayor control sobre el proceso, evita dependencias externas y permite realizar pruebas de manera segura y autónoma. Además, refleja el comportamiento habitual de muchas redes empresariales, donde la instalación de sistemas se realiza en entornos cerrados por motivos de seguridad.

En una implementación real, el servidor podría estar conectado a internet para obtener paquetes actualizados o acceder a repositorios. De todos modos, esta conexión se daría mediante una salida NAT que estaría totalmente controlada por el firewall corporativo de la empresa.

## Comunicaciones internas

Las comunicaciones internas se establecen dentro de la red local (LAN) que conecta el servidor PXE con los equipos clientes, permitiendo la automatización completa del proceso de instalación y configuración de los sistemas operativos Linux.
Esta red interna cumple las siguientes funciones clave:
Asignación dinámica de direcciones IP: El servidor proporciona direcciones IP a los equipos clientes mediante un servidor DHCP configurado para gestionar exclusivamente el rango de la red local. Garantizando una asignación rápida y fiable sin dependencia externa.


*Servicio de arranque en red (PXE)*: Mediante el protocolo TFTP, el servidor entrega a los clientes los archivos necesarios para arrancar el sistema y comenzar la instalación automática del sistema operativo.


*Distribución de imágenes y archivos de instalación*: Las imágenes del sistema y los archivos de configuración se distribuyen a través de protocolos HTTP o NFS, permitiendo un acceso eficiente y escalable para los clientes durante el proceso de instalación.


*Ejecución de scripts de post-instalación y configuración automática*: Tras la instalación inicial, se ejecutan scripts automatizados usando herramientas como cloud-init y Ansible, que configuran los sistemas según los parámetros definidos.


*Seguridad y aislamiento*: Al tratarse de una red interna aislada sin acceso a internet, se minimizan riesgos externos y se mantiene un control total sobre el tráfico y la infraestructura.


*Monitorización y logging*: El servidor registra eventos y estados de las comunicaciones internas para facilitar la detección de errores y el mantenimiento proactivo.


En resumen, esta red interna está diseñada para ser eficiente, segura y totalmente autosuficiente, garantizando un despliegue rápido y fiable en entornos controlados de pruebas o producción.

## Integración de redes y dispositivos

La solución propuesta se apoya en la integración de un servidor central con varios dispositivos cliente dentro de una misma red local, interconectados mediante un switch.
El servidor actúa como punto único de gestión y despliegue, integrando múltiples servicios necesarios para la instalación desatendida de los sistemas operativos:
DHCP: asigna direcciones IP dinámicas a los clientes al arrancar por red.


*TFTP*: proporciona los archivos necesarios para el arranque PXE.


*HTTP*: sirve las imágenes del sistema operativo y los ficheros de configuración (Preseed, cloud-init).


*Ansible*: gestiona la configuración post-instalación de forma centralizada y reproducible.


Todos los dispositivos de la red están conectados directamente al switch, lo que garantiza un tráfico interno rápido, estable y seguro.
Esta integración permite que cualquier equipo conectado a la red pueda ser instalado y configurado automáticamente sin intervención manual, siempre que esté preparado para arrancar por PXE.
