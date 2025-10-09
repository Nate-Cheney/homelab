
This repository contains the configuration and documentation for my homelab.

Each service is managed by it's own docker-compose.yaml file in it's directory. These services are included in the "master" docker-compose.yaml in the root of this repo.

## Access

Cloudflare tunnels are utilized to access each service. The "master" docker-compose.yaml file manages the cloudflared service.

Every application served through a cloudflare tunnel is added to the `homelab-net` docker network. This allows for applications to be referenced by their service name when setting tunnels up in the cloudflared dashboard.

## Documentation

Documentation can be found in the docs directory or [here](./docs/README.md).

