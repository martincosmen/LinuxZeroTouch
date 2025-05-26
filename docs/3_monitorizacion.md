## Monitorización del entorno

Para garantizar la fiabilidad del proceso de instalación automatizada y del servidor que lo implementa, se incorpora un sistema básico de monitorización. Esta monitorización tiene como objetivo detectar posibles fallos o comportamientos anómalos durante el despliegue de los equipos, así como controlar el estado general del servidor.

### Elementos monitorizados

El sistema se centra en los siguientes aspectos:

- **Estado del servidor PXE**: uso de CPU, RAM y disco.
- **Disponibilidad de servicios**: DHCP, TFTP, HTTP.
- **Fallos en el proceso de instalación**: cortes de conexión, errores de scripts de post instalación, instalaciones incompletas.
- **Caídas o reinicios inesperados** del servidor o sus servicios.
- **Consumo de recursos** durante despliegues múltiples simultáneos.

### Herramientas utilizadas

Se emplean herramientas sencillas, ligeras y de fácil integración:

- `htop`: para supervisar en tiempo real el uso de CPU, RAM y procesos activos.
- `journalctl`: para revisar los logs de servicios como `dhcp`, `apache2`, `tftpd-hpa` y detectar errores.
- `logwatch`: para generar informes diarios resumidos sobre el estado del sistema y los servicios críticos.

### Implementación

- **Supervisión manual**: durante los despliegues, se utiliza `htop` en tiempo real para observar el comportamiento del servidor.
- **Verificación automática**: mediante un script programado con `cron`, se comprueba cada cierto tiempo que los servicios clave están activos. Si alguno falla, se escribe una entrada en un log personalizado.
- **Análisis posterior**: tras los despliegues, se revisan los logs de instalación y los resúmenes generados por `logwatch` para comprobar si ha habido errores o eventos anómalos.

---

Esta solución de monitorización es sencilla, pero suficiente para un entorno de pruebas y fácilmente escalable si se quisiera implementar en producción. Permite detectar incidencias de forma rápida, actuar ante fallos y mejorar la fiabilidad del sistema.
