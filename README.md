
## Homelab

This repository contains the configuration and documentation for my homelab.

## Goals

The purpose of my homelab is to learn. It is an environment where I can try new things, make mistakes, practice debugging, and fix issues.

## To-do

- [ ] fail2ban
- [ ] 2fa for ssh

## Overview

Each service is managed by it's own docker-compose.yaml file in it's directory. These services are included in the "master" docker-compose.yaml in the root of this repo.

#### Access

Cloudflare tunnels are utilized to access each service. The "master" docker-compose.yaml file manages the cloudflared service.

Every application served through a cloudflare tunnel is added to the `homelab-net` docker network. This allows for applications to be referenced by their service name when setting tunnels up in the cloudflared dashboard.

#### Hardware

My homelab currently runs on an old `HP ZBook Studio x360 G5` that I got as a give-a-way.

#### Security

###### Firewall

| Port    | Action | From     |
| ------- | ------ | -------- |
| 22      | Allow  | Anywhere |
| 80      | Allow  | Anywhere |
| 443     | Allow  | Anywhere |
| Default | Deny   | Anywhere |

###### SSH

I've hardened SSH by doing the following:
- Preventing root logins.
- Disabled password authentication.
- Disabled empty passwords.
- Limit client inactivity to 5 mins.
- Limit client connections to 2.

## Documentation

For additional documentation, see the `docs` directory. An overview is available in the [README](https://github.com/Nate-Cheney/homelab/tree/main/docs).

