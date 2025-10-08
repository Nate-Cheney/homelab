
Cloudflared is a server-side daemon that tunnels securely routes server traffic through Cloudflare.

The cloudflared service is controlled by the master docker compose file. The homelab-net docker network is utilized so that the tunnel can reference the services by their names rather than a private IP.

## Setup

#### Create a Tunnel

1. Go to the [cloudflare dashboard](https://dash.cloudflare.com/login).
2. Click on Zero Trust.
3. Click on Networks > Tunnels.
4. Click Create a tunnel.
5. Select Cloudflared.
6. Name the tunnel and select Save tunnel.
7. Click Docker, copy the token that precedes the --token flag in the docker run command.
8. Open the .env file in the root of the homelab dir and set the `CF_TOKEN` to the token copied in step 7. 

#### Add a Service

1. Go to the [cloudflare dashboard](https://dash.cloudflare.com/login).
2. Click on Zero Trust.
3. Click on Networks > Tunnels.
4. Go to the desired tunnel on the cloudflare dashboard.
5. Click Edit > Published application routes.
6. Click Add a published application route.
7. Fill out the hostname information as desired.
8. Select the type of service.
9. The URL should be: `{docker compose service name}:{port}`

#### Create an Application

1. Go to the [cloudflare dashboard](https://dash.cloudflare.com/login).
2. Click on Zero Trust.
3. Click on Access > Applications.
4. Click Add an application.
5. Select Self-hosted
6. Enter the desired Application name
7. Set the desired Session Duration
8. Click Add public hostname. **Note**: there will likely be a DNS Record Warning, you can ignore this.
9. Select an existing or create a new access policy.
10. Click next.
11. Customize any of the subsequent options as desired.
12. Make sure to click Save on the Advanced settings (optional) page.

## Environment Variables

`CF_TOKEN` the cloudflare token will be displayed when the tunnel is first created on the zero-trust dashboard. The token should be copied from the docker option. 
    For example: `docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token eyJhIjoiNzJkMjM1NjY0ZWE0ZGI5ZDVmYTExNjg4YjliYmQ1Y2QiLCJ0IjoiNGQ0ZGUyYWQtNTEzOC00NTYwLWE1MWQtZjU0ZWEwMDRlODc1IiwicyI6Ik9ERXhNakV3TWpFdFpHVm1ZUzAwWldKaUxXRmxaR1l0TTJKaE1tUmtOakppT0RB119`


