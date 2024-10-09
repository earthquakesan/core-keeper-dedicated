# Core Keeper Dedicated Server

Notes:

* Install on Ubuntu 22.04 on Hetzner CX32 VM (7.50 Euros per month)
* The docker image used for the deployment: escaping/core-keeper-dedicated

# How To Install

* Install docker
* Run the following commands as root

```
mkdir -p /opt/core-keeper
cat <<EOF > /opt/core-keeper/docker-compose.yml
version: "3"

services:
  core-keeper:
    image: escaping/core-keeper-dedicated
    volumes:
      - /opt/core-keeper/server-files:/home/steam/core-keeper-dedicated
      - /opt/core-keeper/server-data:/home/steam/core-keeper-data
    env_file:
      - ./core.env
    restart: always
    stop_grace_period: 2m
EOF

cat <<EOF > /opt/core-keeper/core.env
ME_ID=
WORLD_INDEX=0
WORLD_NAME=Core Keeper Server
WORLD_SEED=0
MAX_PLAYERS=10
DATA_PATH=/home/steam/core-keeper-data
DISCORD=1
DISCORD_HOOK=https://discord.com/api/webhooks/foo/bar
SEASON=0
EOF

cd /opt/core-keeper
docker compose up -d
```

# How To Use Local Save

* Locate your local save (0.world.gzip file)
* Copy to the server (e.g., using scp)
* Move to the worlds/ dir in server-data

```
ls /opt/core-keeper/server-data/worlds/0.world.gzip
```

* Restart the server

```
cd /opt/core-keeper
docker compose up -d --force-recreate
```

You might want to backup the world save file to a cloud object storage (e.g. Hetzner object storage, S3 bucket etc.)

# Save files

* [09.10.2024](https://1drv.ms/u/s!Ai6a_lE_i0ayhvMDmbpei85eRZ4muw?e=q9MbEa)

All the bosses up to the core keeper are opened (spoiler alert!)
