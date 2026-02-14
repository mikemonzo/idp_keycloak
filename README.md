# keycloak_java

Entorno local de Keycloak con PostgreSQL usando Docker Compose.

## Requisitos

- Docker Desktop (o Docker Engine + plugin Compose)
- Docker Compose v2 (`docker compose`)

## Proceso recomendado para desarrolladores

### 1. Levantar servicios

```bash
docker compose up -d
```

Primera ejecución: descargará imágenes (`postgres:16` y `quay.io/keycloak/keycloak:latest`), puede tardar varios minutos.

### 2. Validar estado de contenedores

```bash
docker compose ps
```

Resultado esperado:

- `keycloak-postgres` en estado `Up ... (healthy)`
- `keycloak` en estado `Up`
- Puerto publicado `0.0.0.0:8080->8080/tcp`

### 3. Validar arranque en logs

```bash
docker compose logs --tail=120 keycloak
```

Busca una línea equivalente a:

- `Keycloak ... started in ... Listening on: http://0.0.0.0:8080`

Opcionalmente, revisar base de datos:

```bash
docker compose logs --tail=80 postgres
```

Debe aparecer:

- `database system is ready to accept connections`

### 4. Acceso a la consola

- URL: `http://localhost:8080`
- Usuario admin: `admin`
- Password admin: `admin`

Nota: en algunos entornos la URL puede tardar unos segundos extra en responder aunque el contenedor ya esté `Up`.

## Parar el entorno

```bash
docker compose down
```

## Reiniciar el entorno

```bash
docker compose down && docker compose up -d
```

## Limpiar volúmenes (borra datos de Postgres)

```bash
docker compose down -v
```

## Troubleshooting rápido

- Si `keycloak` reinicia continuamente:
  - revisar `docker compose logs keycloak`
  - confirmar que `postgres` está `healthy` en `docker compose ps`
- Si no abre `http://localhost:8080`:
  - comprobar que Docker Desktop está iniciado
  - validar que el puerto `8080` no está ocupado por otro servicio
