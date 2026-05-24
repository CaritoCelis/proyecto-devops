# Proyecto DevOps — Innovatech Chile

Aplicación de microservicios contenedorizada con Docker, orquestada con Docker Compose y desplegada automáticamente mediante GitHub Actions.

## Integrantes
- Carolina Celis
- Rodrigo Delgadillo

## Arquitectura

```
frontend (React + Vite) → back1-ventas (Spring Boot) → mysql-ventas
                        → back2-despacho (Spring Boot) → mysql-despacho
```

## Servicios

| Servicio | Tecnología | Puerto |
|---|---|---|
| frontend-devops | React + Vite | 5173 |
| backend-ventas | Spring Boot | 8080 |
| backend-despacho | Spring Boot | 8081 |
| mysql-ventas | MySQL 8 | 3308 |
| mysql-despacho | MySQL 8 | 3309 |

## Requisitos previos

- Docker Desktop instalado
- Git

## Cómo levantar el proyecto

1. Clonar el repositorio:
```bash
git clone https://github.com/CaritoCelis/proyecto-devops.git
cd proyecto-devops
```

2. Crear el archivo `.env` en la raíz:
```env
MYSQL_ROOT_PASSWORD=1234
MYSQL_USERNAME=root
MYSQL_DB_VENTAS=devops_ventas
MYSQL_DB_DESPACHO=devops_despacho
```

3. Levantar todos los servicios:
```bash
docker compose up --build
```

4. Acceder a los servicios:
- Frontend: http://localhost:5173
- API Ventas: http://localhost:8080/swagger-ui.html
- API Despacho: http://localhost:8081/swagger-ui.html

## Estructura del proyecto

```
proyecto-semestral/
├── back1-ventas/          # Microservicio de ventas (Spring Boot)
│   └── Dockerfile         # Multi-stage build
├── back2-despacho/        # Microservicio de despacho (Spring Boot)
│   └── Dockerfile         # Multi-stage build
├── front-despacho/        # Frontend (React + Vite)
│   └── Dockerfile         # Multi-stage build
├── docker-compose.yml     # Orquestación de servicios
├── .env                   # Variables de entorno (no incluido en el repo)
└── .github/
    └── workflows/
        └── deploy.yml     # Pipeline CI/CD
```

## Decisiones técnicas

### Dockerfile multi-stage
Se utilizó multi-stage build en todos los servicios para separar la etapa de compilación del runtime, reduciendo el tamaño final de la imagen y la superficie de ataque.

### Usuario no root
Todos los contenedores corren con un usuario sin privilegios de root, siguiendo el principio de mínimo privilegio.

### Named volumes
Se utilizaron named volumes (`mysql_ventas_data`, `mysql_despacho_data`) en lugar de bind mounts porque:
- Son gestionados por Docker, independientes del sistema de archivos del host
- Persisten los datos aunque el contenedor se elimine
- Son portables entre entornos

### Healthcheck
Los backends esperan que MySQL esté completamente listo antes de iniciar, evitando errores de conexión en el arranque.

### Variables de entorno
Las credenciales se manejan mediante un archivo `.env` excluido del repositorio, nunca hardcodeadas en el código fuente.

## Pipeline CI/CD

El pipeline se activa con cada push a la rama `deploy` y ejecuta 3 jobs en paralelo:

```
push a rama deploy
        ↓
GitHub Actions
        ↓
┌─────────────────┬──────────────────┬─────────────────┐
│  back1-ventas   │  back2-despacho  │  front-despacho │
│  build & push   │  build & push    │  build & push   │
└─────────────────┴──────────────────┴─────────────────┘
        ↓
Docker Hub (imagen:latest + imagen:vN)
```

### Imágenes publicadas en Docker Hub
- `hizaki1/back1-ventas:latest`
- `hizaki1/back2-despacho:latest`
- `hizaki1/front-despacho:latest`

## Seguridad
- Credenciales gestionadas con GitHub Secrets
- Contenedores con usuario no root
- Variables de entorno separadas del código
- `.env` excluido del repositorio via `.gitignore`