"""
## 🧩 4.5 - Software y Paquetes de Software

En este apartado se detalla el conjunto de aplicaciones que se instalarán automáticamente en los equipos según el departamento al que pertenezcan, como parte del sistema de despliegue automatizado de Linux.

Cada equipo contará con un conjunto común de herramientas básicas, y un grupo adicional de aplicaciones específicas en función de su rol dentro de la empresa. Esta estrategia evita la sobrecarga de software innecesario, asegurando un entorno de trabajo eficiente y adaptado.

---

### 🔧 Paquetes Comunes

Todos los equipos, sin importar su departamento, incluirán el siguiente software básico:

- Navegador web: **Firefox**
- Terminal: **GNOME Terminal**
- Configuración entorno: **GNOME Tweaks**
- Ofimática: **Microsoft 365 (E3)**
- Comandos básicos: **curl**, **wget**, **net-tools**
- Cliente SSH: **openssh-client**
- Gestor de archivos: **Nautilus (GNOME)**
- Soporte remoto: **AnyDesk**
- Visor de PDFs: **Evince**
- Capturas de pantalla: **gnome-screenshot**
- Monitoreo del sistema: **gnome-system-monitor**

---

### 💻 Departamento de Desarrollo

> Software orientado a la programación, compilación y pruebas de software.

**Herramientas adicionales:**
- Control de versiones: **Git**
- Editor de código: **Visual Studio Code**
- Lenguaje de programación: **Python 3** y **pip**
- Entorno Java: **OpenJDK**
- Entorno JavaScript: **Node.js** y **npm**
- Contenedores / Virtualización: **Docker**

**Objetivo:**  
Permitir a los desarrolladores programar, compilar y desplegar aplicaciones desde el primer arranque, sin pasos manuales. Cumple el objetivo de automatización del entorno de desarrollo.

---

### 🛠️ Departamento de Administración de Sistemas

> Software orientado a la administración remota, gestión de redes y servicios.

**Herramientas adicionales:**
- Conexión remota: **Remmina**
- Gestión de discos: **GParted**
- Análisis de red: **Wireshark**
- Cliente de bases de datos: **DBeaver**
- Virtualización local: **VirtualBox**
- Monitorización de sistema: **htop**

**Objetivo:**  
Permitir al equipo técnico gestionar sistemas, redes y servicios desde el arranque, facilitando el soporte y mantenimiento inmediato.

---

### 🧾 Departamento de Recursos Humanos

> Software centrado en la gestión documental, comunicación y multimedia.

**Herramientas adicionales:**
- Correo y calendario: **Thunderbird**
- Ofimática de respaldo: **LibreOffice**
- Notas y tareas: **Standard Notes**
- Lector de documentos: **Okular**
- Reproductor multimedia: **VLC**
- Videoconferencias: **Zoom**

**Objetivo:**  
Proporcionar al equipo de RRHH un entorno ágil para trabajar con documentos, coordinar tareas y comunicarse sin obstáculos desde el primer uso.
"""