# keycloak_java

Entorno local de Keycloak con PostgreSQL usando Docker Compose.

## Requisitos

- Docker
- Docker Compose

## Levantar el entorno

```bash
docker compose up -d
```

## Acceso

- Keycloak: http://localhost:8080
- Usuario admin: `admin`
- Password admin: `admin`

## Parar el entorno

```bash
docker compose down
```

## Limpiar volúmenes (opcional)

```bash
docker compose down -v
```
