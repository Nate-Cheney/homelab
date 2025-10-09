
Immich is an open source self-hosted photo and video management solution designed as an alternative to Google Photos.

[Back to README](https://github.com/Nate-Cheney/homelab/tree/main/docs#readme)

## Initial Setup

1. Go to the .env in /immich.
2. Fill out the following environment variables as desired.

## Environment variables

`UPLOAD_LOCATION` the location where uploaded files are stored

`DB_DATA_LOCATION` the location where database files are stored.

`TZ` the timezone. See: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List

`IMMICH_VERSION` the Immich version to use (either release or a specific version like "v1.71.0").

`DB_PASSWORD` the connection secret for postgres. Only use character A-Za-z0-9 without special characters or spaces.

`DB_USERNAME` leave as _postgres_

`DB_DATABASE_NAME` leave as _immich_


