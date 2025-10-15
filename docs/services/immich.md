
Immich is an open source self-hosted photo and video management solution designed as an alternative to Google Photos.

[Back to README](https://github.com/Nate-Cheney/homelab/tree/main/docs#readme)

## Initial Setup

1. Go to the .env in /immich.
2. Fill out the following environment variables as desired.

## Environment variables

```.env

# The location where uploaded files are stored
UPLOAD_LOCATION= 

# The location where database files are stored.
DB_DATA_LOCATION= 

# The desired timezone. See: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
TZ=

# The Immich version to use (either release or a specific version like "v1.71.0")
IMMICH_VERSION=

# The connection secret for postgres. Only use character A-Za-z0-9 without special characters or spaces
DB_PASSWORD=

# Leave as postgres
DB_USERNAME= 

# Leave as immich
DB_DATABASE_NAME=

```

## Backups

While not the ideal [3-2-1 backup strategy](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/), I am using [syncthing](https://docs.syncthing.net/index.html) to copy the `UPLOAD_LOCATION` and `DB_DATA_LOCATION` directories to my PC.

The following steps can be followed to copy my setup.

#### 1. Install required packages

On the server:

``` bash
sudo apt update && sudo apt install -y acl syncthing
```

On the desktop:

``` bash
sudo pacman -Sy syncthing
```

#### 2. Start syncthing

On the server:

``` bash
syncthing -no-browse
```

On the PC:

``` bash
syncthing
```

#### 3. Add the remote devices

On the PC, navigate to the syncthing web-ui: `http://127.0.0.1:8384`. Select _Add Remote Device_, paste in the ID from the server, and enter the desired name.

On the server, run the following to add the PC:

``` bash
syncthing cli config devices add --device-id "DEVICE-ID-HERE" --name "PC Name"
```

On the server, you can verify that the PC was added by running:

``` bash
# Should return both device IDs
syncthing cli config devices list
```

On the PC, you can verify that the server was added by checking the `Remote Devices` section of the syncthing web-ui. It should say _Connected (Unused)_.

#### 4. Add the directories to share

To add the directories, run the following from the server:

``` bash
# Add folders
syncthing cli config folders add --id "immich-library" --path "/path/to/homelab/immich/library"
syncthing cli config folders add --id "immich-postgres" --path "/path/to/homelab/immich/postgres"

# Share folders
syncthing cli config folders "immich-library" devices add --device-id "PC-DEVICE-ID"
syncthing cli config folders "immich-postgres" devices add --device-id "PC-DEVICE-ID"
```

#### 5. Accept the share 

On the PC, navigate to the syncthing web-ui (`http://127.0.0.1:8384`). You will see two new boxes inviting you to accept each share.

Click the green _Share_ button. 

Set the folder path as desired. 

Select _Advanced_ and set _Folder Type_ to `Read Only`.

#### 6. Set ACL permissions

Using acl (installed in step 1) we're going to set permissions for the `/path/to/homelab/immich/postgres` directory. Run the following:

``` bash
# Give your user read and execute permissions recursively
sudo setfacl -R -m u:$USER:rX /path/to/homelab/immich/postgres

# Make sure new files created by postgres also get these permissions
sudo setfacl -R -d -m u:$USER:rX /path/to/homelab/immich/postgres

# Allow syncthing to create its .stfolder marker
sudo setfacl -m u:$USER:rwx  /path/to/homelab/immich/postgres
```

#### 7. Start sync & run as service

In order to start the sync, both clients need to be restarted. `Ctrl + c` to quit syncthing on both the server and PC.

To enable and start syncthing as a service run the following:

``` bash
sudo systemctl enable syncthing@$USER
sudo systemctl start syncthing@$USER
```

Syncthing should now be running as a service and begin syncing everything.

