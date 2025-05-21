# Servicios de Red

En este documento se describen los servicios de red que forman parte fundamental del sistema automatizado de instalación y configuración de equipos Linux. Para cada servicio se detallan los motivos de su inclusión, el software utilizado y los aspectos clave que se configurarán en fases posteriores del proyecto.

## 1. Servicio DHCP

### Motivo de implementación

El servicio DHCP es esencial para asignar direcciones IP automáticamente a los equipos cliente en el momento del arranque por PXE.  
Sin este servicio, cada máquina requeriría configuración manual de red, lo que rompería con el enfoque automatizado de todo el sistema.

### Software empleado

- `isc-dhcp-server`

### Aspectos destacables de la configuración

*Pendiente de configuración*  
Se especificarán detalles como el rango de IPs, la interfaz de red usada, y las opciones necesarias para PXE (como el filename y el next-server).

## 2. Servicio TFTP

### Motivo de implementación

TFTP se encarga de transferir los archivos mínimos necesarios para que los equipos cliente puedan arrancar por red.  
Sin este servicio, los equipos no podrían iniciar el proceso de instalación automatizado, obligando al uso de dispositivos físicos como USBs o DVDs.

### Software empleado

- `tftpd-hpa`

### Aspectos destacables de la configuración

*Pendiente de configuración*  
Incluye la ruta de los archivos de arranque (como `pxelinux.0` o `bootx64.efi`) y permisos adecuados para lectura.

## 3. Servicio HTTP

### Motivo de implementación

HTTP se usa para servir las imágenes ISO del sistema operativo y archivos de configuración (como Preseed o scripts de cloud-init).  
Sin este servicio, los clientes no podrían descargar los archivos necesarios para completar la instalación de manera desatendida.

### Software empleado

- `Apache2`

### Aspectos destacables de la configuración

*Pendiente de configuración*  
Incluye la ubicación de los archivos ISO, configuración de los permisos y organización del árbol de directorios para facilitar el acceso desde los clientes.


## 4. Cloud-init y Ansible

### Motivo de implementación

Estas herramientas automatizan la configuración posterior a la instalación, como la creación de usuarios, instalación de software, cambios de red, etc.  
Sin ellas, toda la post-instalación debería hacerse manualmente, lo que anula la automatización total del sistema.

### Software empleado

- `cloud-init`
- `Ansible`

### Aspectos destacables de la configuración

*Pendiente de configuración*  
Se documentará el uso de metadatos en cloud-init y la estructura de los playbooks de Ansible en la fase de configuración.

## 5. Servicio FAI (Fully Automatic Installation)

### Motivo de implementación

Componente principal que permite realizar instalaciones automáticas y desatendidas del sistema operativo en los equipos cliente.  
Se encarga de aplicar configuraciones específicas en función del tipo de equipo o del departamento al que pertenece, automatizando el proceso completo desde el particionado del disco hasta la instalación de paquetes y la configuración inicial.

Sin FAI, sería necesario realizar múltiples instalaciones manuales o mantener plantillas estáticas difíciles de adaptar y escalar, perdiendo toda la ventaja de automatización flexible.

### Software empleado

- `fai-server`
- `fai-setup-storage`
- `fai-mirror`

### Aspectos destacables de la configuración

*Pendiente de configuración*  
La estructura de clases (`classes`), scripts de instalación, configuración de particionado (`disk_config`) y listas de paquetes se definirá para cubrir los distintos perfiles de usuario (desarrollador, administración, RRHH).  
FAI se integrará con PXE y el resto de servicios para lanzar automáticamente la instalación según el rol asignado a cada equipo.

