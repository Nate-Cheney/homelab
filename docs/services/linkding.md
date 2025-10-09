
Linkding is a self hosted bookmark manager.

[Back to README](https://github.com/Nate-Cheney/homelab/tree/main/docs#readme)

## Setup

1. No .env configuration required
2. Start containers
3. Create a user with `docker exec -it linkding python manage.py createsuperuser --username=[username] --email=[email]`
4. Enter a password

#### Linkding Browser Plugin

1. Sign into linkding.
2. Click Settings > Admin.
3. Click Add under AUTH TOKEN.
4. Select the desired user.
5. Click SAVE.
6. Copy the token.
7. Install the linkding extension for either Chrome or Firefox.
8. Click on the extension and then get started.
9. Enter the URL for your instance of linkding.
10. Enter the API copied in step 6.
11. Change any of the desired options.

## Environment Variables

None

