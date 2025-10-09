
This directory contains all necessary documentation to maintain my homelab.

## services

The services directory describes the configuration and start process for each service.

[cloudflared](https://github.com/Nate-Cheney/homelab/blob/main/docs/services/cloudflared.md)

[homepage](https://github.com/Nate-Cheney/homelab/blob/main/docs/services/homepage.md)

[immich](https://github.com/Nate-Cheney/homelab/blob/main/docs/services/immich.md)

## update

Simply running the following from the root of the homelab directory will pull the most up-to-date version of each container and start them:

```bash
docker compose pull && docker compose up -d
```

