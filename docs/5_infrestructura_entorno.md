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
  - CPU: 2 vCore
  - RAM: 4 GB
  - Disco duro: 50 GB
  - Adaptador de red: Red interna (para recibir configuración y sistema vía PXE)

- **Propósito:**
  - Verificar el correcto funcionamiento de la instalación automatizada.
  - Validar la instalación personalizada de paquetes para cada departamento.

 ## 2. Estaciones de trabajo

En un escenario real de implementación, cada estación de trabajo estaría equipada con hardware físico adaptado a las necesidades específicas del departamento correspondiente. No obstante, en este proyecto todas las pruebas se realizan mediante máquinas virtuales en VirtualBox, con configuraciones iguales y simplificadas para simular correctamente el proceso de despliegue automatizado.

A continuación se detallan las configuraciones recomendadas que podrían utilizarse en una implantación real en función del perfil profesional:

### Departamento de Desarrollo

Equipos con mayor capacidad de procesamiento y memoria para compilar código, ejecutar entornos de desarrollo, máquinas virtuales o contenedores.

- **Procesador:** Intel Core i7 o AMD Ryzen 7  
- **Memoria RAM:** 32 GB  
- **Disco duro:** SSD de 1 TB  
- **Tarjeta gráfica:** Básica, con soporte para herramientas gráficas  
- **Conectividad:** Ethernet y Wi-Fi  
- **Periféricos:** Teclado, ratón y monitor

### Departamento de Administración de Sistemas

Equipos preparados para la gestión de redes y sistemas, con recursos adecuados para ejecutar máquinas virtuales y herramientas de monitorización.

- **Procesador:** Intel Core i5 o AMD Ryzen 5  
- **Memoria RAM:** 16 GB  
- **Disco duro:** SSD de 512 GB  
- **Tarjeta gráfica:** Integrada  
- **Conectividad:** Ethernet y Wi-Fi  
- **Periféricos:** Teclado, ratón y monitor

### Departamento de Recursos Humanos

Equipos con requerimientos básicos, centrados en tareas de gestión documental, comunicación y ofimática.

- **Procesador:** Intel Core i5 o AMD Ryzen 5  
- **Memoria RAM:** 8–16 GB  
- **Disco duro:** SSD de 256–512 GB  
- **Tarjeta gráfica:** Integrada  
- **Conectividad:** Ethernet y Wi-Fi  
- **Periféricos:** Teclado, ratón y monitor

 **Observación:** Aunque estas configuraciones representan una propuesta realista para su uso en producción, el entorno del proyecto se limita al uso de máquinas virtuales con especificaciones más reducidas, suficientes para demostrar la viabilidad del sistema de instalación y configuración automatizada.
 