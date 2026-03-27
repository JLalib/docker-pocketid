# Pocket ID

Este repositorio contiene las instrucciones para desplegar **Pocket
ID**, un sistema de autenticación moderno basado en **WebAuthn**,
utilizando **Docker Compose**.

Pocket ID permite autenticación segura sin contraseñas (passwordless),
ideal para homelab y entornos empresariales.

Repositorio oficial: https://github.com/pocket-id/pocket-id

------------------------------------------------------------------------

## ⚠️ Requisito importante

Pocket ID **requiere HTTPS obligatorio**.

Esto se debe a que utiliza la API **WebAuthn**, que solo funciona en
contextos seguros.

Opciones recomendadas:

-   Reverse proxy (Caddy, Nginx, Traefik)
-   Cloudflare Tunnel
-   Certificados TLS propios (Let's Encrypt)

------------------------------------------------------------------------

## 🚀 Instalación con Docker (recomendada)

### 1️⃣ Descargar archivos necesarios

``` bash
curl -o docker-compose.yml https://raw.githubusercontent.com/pocket-id/pocket-id/main/docker-compose.yml
curl -o .env https://raw.githubusercontent.com/pocket-id/pocket-id/main/.env.example
```

------------------------------------------------------------------------

### 2️⃣ Editar el fichero `.env`

Genera la clave hash: 

``` bash
openssl rand -base64 32
```

Configura al menos:

``` env
APP_URL=https://tu-dominio.com

ENCRYPTION_KEY=
```

------------------------------------------------------------------------

### 3️⃣ Arrancar el servicio

``` bash
docker compose up -d
```

------------------------------------------------------------------------

## 🌐 Acceso inicial

Accede a:

    https://TU-DOMINIO/setup

------------------------------------------------------------------------

## 🐳 docker-compose.yml (ejemplo básico)

``` yaml
services:
  pocket-id:
    image: ghcr.io/pocket-id/pocket-id:latest
    container_name: pocket-id
    restart: unless-stopped
    env_file:
      - .env
    ports:
      - "3000:3000"
```

------------------------------------------------------------------------

## 🔧 Variables de entorno comunes

  Variable       Descripción
  -------------- --------------------------
  APP_URL        URL pública HTTPS
  JWT_SECRET     Clave de seguridad
  DATABASE_URL   Conexión a base de datos

------------------------------------------------------------------------

## ▶️ Comandos útiles

``` bash
docker compose up -d
docker compose logs -f
docker compose restart
docker compose down
```

------------------------------------------------------------------------

## 🔄 Actualizar

``` bash
docker compose pull
docker compose up -d
```

------------------------------------------------------------------------

## ⚠️ Seguridad

-   HTTPS obligatorio
-   No exponer sin proxy
-   Usar firewall o VPN

------------------------------------------------------------------------

