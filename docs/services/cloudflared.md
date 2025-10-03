
Cloudflared is a server-side daemon that tunnels securely routes server traffic through Cloudflare.

The cloudflared service is controlled by the master docker compose file. The homelab-net docker network is utilized so that the tunnel can reference the services by their names rather than a private IP.

## Environment Variables

`CF_TOKEN` the cloudflare token will be displayed when the tunnel is first created on the zero-trust dashboard. The token should be copied from the docker option. 
    For example: `docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token eyJhIjoiNzJkMjM1NjY0ZWE0ZGI5ZDVmYTExNjg4YjliYmQ1Y2QiLCJ0IjoiNGQ0ZGUyYWQtNTEzOC00NTYwLWE1MWQtZjU0ZWEwMDRlODc1IiwicyI6Ik9ERXhNakV3TWpFdFpHVm1ZUzAwWldKaUxXRmxaR1l0TTJKaE1tUmtOakppT0RB119`


