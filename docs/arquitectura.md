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

```markdown
![Diagrama de Red](docs/pics/diseño-red.PNG)

