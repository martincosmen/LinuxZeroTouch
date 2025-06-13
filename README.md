# Configuración del servidor PXE

Este repositorio contiene todos los ficheros utilizados en la configuración del servidor PXE para el despliegue automatizado de sistemas operativos mediante cloud-init y Ansible.

## Estructura del repositorio

- `ficheros-configuracion/ansible/`: Contiene el playbook, inventario y configuración de Ansible utilizados para instalar y configurar automáticamente los paquetes y servicios necesarios en los clientes.

- `ficheros-configuracion/cloud-init/`: Archivos `user-data` y `meta-data` utilizados por cloud-init durante la instalación automática de los sistemas operativos.

- `ficheros-configuracion/pxe/`: Ficheros esenciales del arranque por red PXE/iPXE, incluyendo el script `boot.ipxe`, el kernel (`vmlinuz`), el initramfs (`initrd`) y otros recursos necesarios para el despliegue.

---

Este repositorio está orientado exclusivamente al despliegue automatizado en una red local simulada. Puedes adaptarlo a tus necesidades o entorno real.