# Proyecto DevOps - Microservicios con Docker Compose

## Descripción

Proyecto desarrollado utilizando arquitectura de microservicios, contenedores Docker y Docker Compose para automatizar el despliegue de servicios.

El sistema está compuesto por:

* Frontend desarrollado con React + Vite
* Microservicio de Ventas desarrollado con Spring Boot
* Microservicio de Despacho desarrollado con Spring Boot
* Base de datos MySQL 8

## Tecnologías utilizadas

* Docker
* Docker Compose
* Spring Boot
* Java 17
* MySQL
* React
* Vite
* GitHub
* Postman

## Arquitectura

Frontend React/Vite
↓
Backend Ventas (Spring Boot)
Backend Despacho (Spring Boot)
↓
MySQL 8

## Ejecución del proyecto

### Clonar repositorio

```bash
git clone https://github.com/CaritoCelis/proyecto-devops.git
```

### Ingresar al proyecto

```bash
cd proyecto-devops
```

### Levantar contenedores

```bash
docker compose up -d
```

## Puertos utilizados

* Frontend: 5173
* Backend Ventas: 8080
* Backend Despacho: 8081
* MySQL: 3308

## Objetivo DevOps

El objetivo del proyecto fue implementar un entorno automatizado utilizando contenedores Docker, facilitando el despliegue, la portabilidad, la escalabilidad y la administración de servicios mediante prácticas DevOps.
