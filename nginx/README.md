NGINX REVERSE PROXY SETUP DOCUMENTATION

1. Overview

This guide documents the setup of a nginx reverse proxy to route traffic to internal services using domain names, with support for Docker integration.

Nginx is running as a Docker container with dynamic configuration via Docker labels and DNS-based service access.

2. Prerequisites

- Docker 
- Docker Compose v2+
- Domain / subdomain pointing to the server’s IP or internal DNS record.In our case, api-william.esoko.com and web-william.esoko.com both pointing the server IP 10.1.1.221
- Open ports:
80 (HTTP)
80:80(Nginx Reverse Proxy)
8090:80(Push-API)
8080:3000(Push-WEB)

3. Project Directory Structure

nginx/
├── docker-compose.yml
├── reverse-proxy/
│   ├── Dockerfile
│   ├── push.conf
│   └── nginx.conf
└── README.md

4. Deploying the Setup

docker compose up -d

5.Accessing the Services

To access push web:
http://web-william.esoko.com:8080

To access push api:
http://api-william.esoko.com:8090

To access nginx:
http://localhost:80

To stop service:

docker compose down


