
RustDesk is remote access and support software.

[Back to README](https://github.com/Nate-Cheney/homelab/tree/main/docs#readme)

## Setup

1. No .env configuration required
2. Start containers
3. Check container logs for the server key

#### RustDesk Client Configuration 

1. Go to Settings > Network
2. Unlock network settings
3. Select _ID/Relay server_
4. Enter the Tailscale IP in the _ID server_ and _Relay server_ options
5. Enter the key saved in Setup > Step 3
6. Add other clients and connect to them as normal

## Environment Variables

None

