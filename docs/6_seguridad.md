# Seguridad

La seguridad del sistema se ha diseñado considerando distintos niveles de protección: acceso desde el exterior, control interno, protección perimetral y medidas de respaldo. Aunque el entorno es de pruebas, se aplican buenas prácticas básicas que pueden escalarse a entornos reales.

## ▪ Mecanismos de vigilancia y acceso desde el exterior y zonas restringidas en el interior

**Acceso remoto restringido:**  
El servidor solo permite conexiones SSH desde direcciones IP internas autorizadas. Se ha deshabilitado el acceso root remoto y se obliga al uso de claves SSH en lugar de contraseñas.

**Supervisión de accesos:**  
Se revisa el archivo `/var/log/auth.log` para detectar intentos de acceso no autorizados. También se utiliza `journalctl` y `logwatch` para obtener resúmenes de actividad del sistema.

**Cortafuegos con iptables:**  
Se utiliza un firewall básico con `iptables` que permite únicamente los puertos necesarios (67/UDP DHCP, 69/UDP TFTP, 80/TCP HTTP, 22/TCP SSH), bloquea el resto del tráfico entrante o saliente innecesario y filtra conexiones no deseadas desde direcciones externas.

---

## ▪ Seguridad perimetral

**Aislamiento de red:**  
Los equipos cliente están conectados a una red interna aislada sin acceso a Internet. Solo el servidor dispone de doble interfaz de red para gestionar tanto la red interna como una salida controlada al exterior.

**Conexión a Internet controlada:**  
Si el servidor necesita conectarse a Internet (por ejemplo, para actualizaciones), se hace mediante NAT bajo reglas estrictas del firewall. No se exponen servicios a Internet en ningún momento.

---

## ▪ Seguridad interna

**Control de servicios:**  
Solo están activos los servicios estrictamente necesarios: DHCP, TFTP, HTTP y SSH. El resto están deshabilitados para reducir la superficie de ataque.

**Principio de mínimos privilegios:**  
Los usuarios trabajan sin permisos de root. Las tareas administrativas requieren el uso de `sudo`, lo que permite registrar y auditar su uso.

**Protección de scripts y configuraciones:**  
Todos los scripts, ficheros de configuración y credenciales están protegidos con permisos restrictivos (`chmod 600` o `chmod 700`).

**Registros de actividad:**  
Se conservan logs de accesos, fallos de servicios y eventos del sistema para facilitar auditorías y detectar incidentes.

---

## ▪ Copias de seguridad: cómo, dónde, cuándo

**¿Qué se respalda?**

- Configuraciones de servicios (DHCP, TFTP, Apache, FAI…)
- Scripts de instalación (`preseed`, `cloud-init`, `Ansible`)
- Logs de despliegue
- Imágenes ISO utilizadas

**¿Cómo?**  
Se utiliza un script automatizado que empaqueta y guarda los archivos en una carpeta de respaldo comprimida.

**¿Dónde?**  
Inicialmente, en una segunda partición o disco local. En un entorno real, podrían almacenarse en un servidor externo o unidad de red.

**¿Cuándo?**  

- Diariamente durante la fase de pruebas.
- Antes y después de cada despliegue en producción.
