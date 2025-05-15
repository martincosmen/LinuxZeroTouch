# 4.4 Base de datos

## Introducción

Aunque este proyecto no se centra en el desarrollo de una aplicación web o un sistema que requiera una base de datos funcional, se incluye un modelo Entidad/Relación (E/R) que representa de forma conceptual el modelo de negocio relacionado con el entorno de automatización de instalaciones en una empresa de soporte técnico como PLEXUS TECH.

## Modelo Entidad/Relación

El siguiente esquema representa las relaciones principales entre los elementos que intervienen en la automatización del proceso de instalación y configuración de equipos.

![Modelo ER](../pics/modelo_er.png)

## Descripción de las entidades

- **Equipo**  
  Contiene información de cada equipo cliente a instalar. 
  
  Campos: `ID_Equipo`, `Hostname`, `Mac_address`, `Departamento`, `Fecha_registro`.

- **Imagen**  
  Representa las imágenes de sistemas disponibles. 
  
  Campos: `ID_Imagen`, `Nombre`, `Version`, `Tipo de sistema`, `Fecha_creacion`, `tipo`, `ruta`.

- **Instalación**  
  Registra cada proceso de instalación realizado. 
  
  Campos: `fk_ID_Equipo`, `fk_ID_Imagen`, `Fecha`, `Resultado`.

- **Técnico**  
  Representa a los técnicos encargados del despliegue o mantenimiento. Relacionado con las instalaciones realizadas.

## Observaciones

- Este modelo es solo conceptual y tiene como objetivo representar cómo se gestionaría la automatización si se necesitase persistencia de datos.
- No se implementará físicamente ninguna base de datos como parte del despliegue técnico del proyecto.
