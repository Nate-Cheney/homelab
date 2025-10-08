
This repository contains the configuration and documentation for my homelab.

Each service is managed by it's own docker-compose.yaml file in it's directory.

## Access

Cloudflare tunnels are utilized to access each service. The docker-compose.yaml file in the root of the repo manages the cloudflared service.

Every application served through a cloudflare tunnel is added to the `homelab-net` docker network. This allows for applications to be referenced by their service name when setting tunnels up in the cloudflared dashboard.

## Documentation

INSERT LINK TO docs/README.md here
