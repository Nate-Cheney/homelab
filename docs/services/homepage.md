
Homepage is a highly customizable application dashboard with built in integrations for a number of services. Homepage is configured via YAML files.

[Back to README](https://github.com/Nate-Cheney/homelab/tree/main/docs#readme)

## Initial Setup

1. Go to the .env file in /homepage.
2. Add the private IP address and hostname of the server (both followed by :3000) to the `HOMEPAGE_ALLOWED_HOSTS` variable.
3. Add the domain that will be used to access homepage to the `HOMEPAGE_ALLOWED_HOSTS` variable.
4. Configure homepage using the documentation [here](https://gethomepage.dev/configs/settings/) as desired.

## Environment Variables

```.env

# A comma separated list of all addresses and domains that should be allowed to access homepage.
HOMEPAGE_ALLOWED_HOSTS

# The user ID of the user that runs the homepage service instead of as root.
PUID

# The group ID of the user that runs the homepage service instead of as root.
PGID

```

