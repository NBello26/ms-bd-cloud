# 🗄️ SanosDB - Persistencia de Datos (PostgreSQL)

Este repositorio gestiona la infraestructura de la base de datos relacional para el ecosistema de gestión de mascotas. Utiliza **PostgreSQL** dockerizado, configurado para servir a los múltiples microservicios que requieren persistencia de datos (Mascotas, Usuarios, etc.).

## 🚀 Arquitectura y Prácticas DevOps

Desde la perspectiva de infraestructura, la base de datos está aislada dentro de la red interna de AWS, permitiendo conexiones únicamente desde las instancias EC2 que ejecutan los microservicios autorizados.

El despliegue está automatizado mediante un pipeline de **CI/CD** con GitHub Actions:
1. Construye una imagen personalizada de Docker con las configuraciones iniciales de PostgreSQL.
2. Sube la imagen a **Amazon Elastic Container Registry (ECR)**.
3. Despliega y reinicia el contenedor en la instancia **EC2** dedicada mediante **AWS Systems Manager (SSM)**.
4. Gestiona volúmenes de Docker para asegurar que los datos persistan incluso si el contenedor se reinicia o actualiza.

### 🌐 Ecosistema de Infraestructura en AWS
La base de datos centraliza la información de toda la arquitectura:

* **Nodo Web:** ApiGateway y Frontend
* **Nodo Back 1:** Eureka Server y BFF
* **Nodo Back 2:** Microservicios de Mascotas y Usuarios
* **Nodo Back 3:** Microservicios de Geolocalización y Notificaciones
* **Nodo Back 4:** Motor de Coincidencias
* **Base de Datos:** **SanosDB (PostgreSQL)** (Este repositorio) 📍

## 🛠️ Tecnologías Principales

* **Motor de Base de Datos:** PostgreSQL 15+
* **Contenedores:** Docker (Alpine based)
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Configuración y Seguridad

* **Aislamiento:** El contenedor de la base de datos no tiene IP pública. Solo es accesible a través de la red privada de AWS para los microservicios del ecosistema.
* **Persistencia:** Se utilizan `Docker Volumes` mapeados a la instancia EC2 para garantizar la integridad de los datos de SanosDB.
* **Inyección de Secretos:** Las credenciales (usuario, password, nombre de la DB) se inyectan dinámicamente en el tiempo de despliegue a través de secretos de GitHub y variables de entorno en el pipeline de DevOps.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III)
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III)

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III) *(Estás aquí)*

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III)
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III)
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III)

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
