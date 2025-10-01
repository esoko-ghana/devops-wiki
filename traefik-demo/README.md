NGINX REVERSE PROXY SETUP DOCUMENTATION

1. Overview

This guide documents the setup of a traefik reverse proxy to route traffic to internal services using domain names, with support for Docker integration.

Traefik is running as a Docker container with dynamic configuration via Docker labels and DNS-based service access.

2. Prerequisites

- Docker 
- Docker Compose v2+
- Domain / subdomain pointing to the server’s IP or internal DNS record.In our case, api-william.esoko.com and web-william.esoko.com both pointing the server IP 10.1.1.221
- Open ports:
80 (HTTP)
443 (HTTPS)
8080 (Traefik)
9090(Push-API)
3000(Push-WEB)

3. Project Directory Structure

traefik-demo/
├── docker-compose.yml
├── traefik/
│   └── traefik.yml

4. Deploying the Setup

docker compose up -d

5.Accessing the Services

To access push web:
http://web-william.esoko.com:3000

To access push api:

http://api-william.esoko.com:9090

To access the traefik dashboard:
http://10.1.1.221:8080/dashboard


To view Logs:

docker logs traefik -f

To stop service:

docker compose down


