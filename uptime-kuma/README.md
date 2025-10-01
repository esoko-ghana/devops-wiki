**Uptime Kuma Deployment with Docker Compose Documentation**

***Overview***

Uptime Kuma is a self-hosted monitoring tool, It allows you to track uptime, response time, and service availability for websites, APIs, servers, and other networked resources.
This guide shows how to deploy Uptime Kuma on TestServer – 10.1.1.221 using a simple Docker Compose configuration.

***Prerequisites***
    • A Linux server or VM (Ubuntu Server OS)
    • Docker installed
    • Docker Compose installed

***Directory Setup***

Create a directory to store Uptime Kuma’s persistent data:
- sudo mkdir -p /srv/uptime-kuma/data
- sudo chown -R $USER:$USER /srv/uptime-kuma/data

This ensures monitoring data (settings, logs, databases) are stored outside the container.

The directory should be structured as:
/srv/
└── uptime-kuma/
    ├── data/                  
    └── docker-compose.yml   

***Docker Compose Configuration***
Save the following configuration as docker-compose.yml:

version: '3.8'
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    volumes:
      - /srv/uptime-kuma/data:/app/data
    ports:
      - "82:3001"
    restart: always

***Explanation of Configuration***

    • version: '3.8' → Docker Compose file format version.
    • image: louislam/uptime-kuma → Official Uptime Kuma Docker image.
    • container_name: uptime-kuma → Gives the container a fixed, recognizable name.
    • volumes → Maps /srv/uptime-kuma/data on the host to /app/data in the container (persistent storage).
    • ports: "82:3001"  Maps host port 82 to container port 3001 (default Kuma web UI).
    • restart: always → Ensures container auto-restarts on reboot or failure.

***Deploying Uptime Kuma***

Run:
docker-compose up -d

Check container status:
docker ps

Logs :
docker logs -f uptime-kuma

Access the Dashboard

Once running, open a browser and go to:
http://10.1.1.221:82

You’ll be prompted to create an admin account on first launch.

***Managing Uptime Kuma***

    • Start service:
      docker-compose up -d

    • Stop service:
      docker-compose down

    • Update to latest version:
      docker-compose pull
      docker-compose up -d

***Best Practices***
    • Regularly back up /srv/uptime-kuma/data.
    • Limit firewall access if exposed to the internet or place it behind the Esoko VPN and configure the firewall to only allow connections from the VPN subnet.

You now have Uptime Kuma running with Docker Compose, ready to monitor your infrastructure and services.
