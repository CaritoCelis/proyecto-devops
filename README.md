# Proyecto DevOps - Innovatech Chile

## Descripción

Este proyecto corresponde a la Evaluación Parcial N°2 de la asignatura Introducción a Herramientas DevOps.

El sistema implementa una arquitectura basada en microservicios utilizando Docker, Docker Compose, AWS EC2 y GitHub Actions para automatizar el despliegue continuo.

---

## Tecnologías utilizadas

- Spring Boot
- MySQL
- Docker
- Docker Compose
- GitHub Actions
- AWS EC2
- Swagger
- GitHub

---

## Arquitectura del proyecto

El proyecto está compuesto por:

- Frontend
- Backend Ventas
- Backend Despachos
- Base de datos MySQL

---

## Contenedorización

Cada servicio cuenta con:

- Dockerfile multi-stage
- Usuario no root
- Variables de entorno
- Puertos expuestos
- Persistencia mediante volúmenes Docker

---

## Ejecución local

```bash
docker compose up -d
```

---

## Persistencia de datos

Se utilizan volúmenes Docker para asegurar que la información no se pierda tras reiniciar contenedores.

---

## Pipeline CI/CD

El proyecto utiliza GitHub Actions para:

- Construcción automática de imágenes Docker
- Publicación en Docker Hub
- Despliegue automático en AWS EC2

---

## Despliegue en AWS

- Frontend desplegado en instancia pública
- Backend desplegado en subred privada
- Comunicación segura mediante Security Groups

---

## Integrantes

- Carolina Celis
- Rodrigo Delgadillo