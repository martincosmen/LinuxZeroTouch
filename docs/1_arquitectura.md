# Arquitectura del Sistema

Este documento describe la arquitectura general del sistema automatizado de instalación y configuración de Linux.  
Incluye una visión general de los componentes clave, como el servidor PXE, el proceso de instalación con Preseed, la configuración con cloud-init y Ansible, y cómo se integran todas las partes para proporcionar una solución escalable y eficiente.

## Diseño de Red

La arquitectura de red propuesta se basa en un entorno local (LAN) donde un servidor central será el encargado de ofrecer servicios de arranque por red (PXE) y automatización de la instalación de sistemas operativos Linux.

Este servidor cuenta con dos interfaces de red:

- Una interfaz conectada a Internet, que le permite obtener paquetes, dependencias y actualizaciones necesarias para los despliegues.
- Una interfaz conectada a una red interna aislada, por donde se comunican los equipos cliente que van a ser instalados.

El diseño está pensado para un entorno de pruebas con máquinas virtuales, aunque es completamente aplicable a entornos físicos. Los clientes se conectan a la red interna, arrancan mediante PXE y reciben automáticamente el sistema operativo y su configuración.

## Componentes de la Red

- **Servidor PXE**
- **Switch**
- **Equipos Linux (3)**

## Justificación del uso de Switch

La elección de un switch en lugar de un router se debe a:

- Mayor control sobre redes locales.
- No es necesario que actúe como puerta de enlace a Internet.
- Permite aislar completamente a los equipos cliente del exterior.
- Refleja una arquitectura común en entornos empresariales reales.

Aunque el entorno planteado es de pruebas, este diseño es perfectamente aplicable a entornos reales. En muchas empresas, los switches permiten interconectar servidores y clientes en redes LAN donde se realiza el despliegue de sistemas, manteniendo la red controlada y segura.

## Diagrama lógico de red

![Diagrama de red](/docs/pics/diagrama_red.png)

## Comunicaciones externas

El servidor PXE tiene acceso a Internet mediante una de sus interfaces de red. Esto permite que:

- Pueda descargar paquetes y actualizaciones desde los repositorios oficiales.
- Se instalen herramientas necesarias para la automatización.
- Se mantenga el sistema actualizado y funcional en todo momento.

Esta conexión a Internet no se extiende a los clientes, que están completamente aislados del exterior. De esta forma se mantiene la seguridad, se evitan interferencias externas y se garantiza que los procesos de instalación se realicen en un entorno controlado.

## Comunicaciones internas

Las comunicaciones internas se realizan dentro de la red local (LAN) entre el servidor PXE y los equipos cliente. Esta red cumple las siguientes funciones clave:

- **Asignación dinámica de IPs**: El servidor gestiona un servicio DHCP que asigna direcciones IP a los clientes en el momento del arranque.
- **Arranque PXE**: A través del protocolo TFTP, el servidor entrega los archivos necesarios para iniciar el sistema e iniciar la instalación automática.
- **Distribución de imágenes y configuración**: Las imágenes del sistema operativo y archivos de configuración (como Preseed y cloud-init) se distribuyen vía HTTP.
- **Post-instalación y configuración automática**: Una vez instalado el sistema, se ejecutan scripts automatizados y configuraciones con Ansible para preparar el entorno del usuario.
- **Aislamiento total**: Al estar en una red interna sin acceso a Internet, los equipos cliente están protegidos de amenazas externas y el entorno es completamente reproducible.

## Integración de redes y dispositivos

La solución integra un servidor central con varios clientes dentro de una red LAN, todos interconectados mediante un switch.

El servidor actúa como núcleo del sistema y ofrece los siguientes servicios:

- **DHCP**: asignación de direcciones IP en la red interna.
- **TFTP**: entrega de archivos necesarios para el arranque PXE.
- **HTTP**: distribución de imágenes del sistema y configuraciones automatizadas.
- **Preseed**: configuración de instalación desatendida de Ubuntu.
- **cloud-init** y **Ansible**: automatización de tareas post-instalación.

Todos los dispositivos están conectados directamente al switch, garantizando un entorno de red eficiente, seguro y completamente gestionado desde el servidor.  
Esto permite que cualquier equipo conectado pueda ser instalado y configurado automáticamente sin intervención manual, siempre que esté preparado para arrancar mediante PXE.
