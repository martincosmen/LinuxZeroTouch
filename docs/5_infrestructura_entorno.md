# Infraestructura y Entorno

En esta sección se detalla el entorno técnico y de ejecución del proyecto, tanto a nivel de hardware como de la distribución lógica de los servicios.

## 1. Infraestructura Hardware

La instalación del sistema se realiza en un entorno **on-premise**, mediante máquinas virtuales creadas en VirtualBox simulando servidores y estaciones de trabajo.

A continuación se describe el servidor principal utilizado para centralizar los servicios de red y desplegar los sistemas operativos de manera automatizada:

### Servidor PXE / FAI

- **Modelo de máquina virtual:** Debian Server 22.04
- **Configuración hardware:**
  - CPU: 2 vCores
  - RAM: 4 GB
  - Disco duro: 50 GB
  - Adaptador de red: Red interna (modo puente para acceso desde clientes)
- **Servicios alojados:**
  - Servidor DHCP
  - Servidor TFTP
  - Servidor HTTP
  - Servidor FAI
  - Cloud-init
  - Ansible
- **Virtualización / contenedores:**
  - No se emplea virtualización bare-metal ni contenedores en el despliegue de servicios. Todos los servicios corren directamente sobre el sistema anfitrión del servidor PXE.

### Equipos Cliente (Desarrollo, Sistemas, RRHH)

Se crean varias máquinas virtuales para simular los equipos de los distintos departamentos que se desplegarán automáticamente mediante PXE y configuración post-instalación.

- **Modelo de máquina virtual:** VirtualBox (Ubuntu Desktop)
- **Cantidad de máquinas:** 3 (una por departamento)
- **Configuración hardware (por equipo):**
  - CPU: 1 vCore
  - RAM: 2 GB
  - Disco duro: 30 GB
  - Adaptador de red: Red interna (para recibir configuración y sistema vía PXE)
- **Propósito:**
  - Verificar el correcto funcionamiento de la instalación automatizada.
  - Validar la instalación personalizada de paquetes para cada departamento.