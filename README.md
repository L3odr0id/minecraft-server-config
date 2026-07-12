# minecraft-server-config

This setup is the ultimate solution: it automatically downloads the latest backup, fetches the server and mods, creates backups regularly, and uploads them to Docker Hub.

# How to run
1. Set env variables:
- `CF_API_KEY` - The API key from CurseForge Studio.
- `MC_DATA_PATH` - The relative path to the Minecraft world directory.
- `MC_BACKUPS_PATH` - The relative path to the backups folder.
- `MC_SERVER_PORT` - The server port.
- `HUB_REPO_NAME` - The Docker Hub repository for fetching and uploading backups Format 'NICKNAME/REPO_NAME'
- `HUB_LOGIN` - Your Docker Hub username.
- `HUB_PASSWORD` - Your Docker Hub access token.
- `DOCKER_IMAGE_TO_PULL` - The name of the Docker image to pull. Format: 'NICKNAME/REPO_NAME:TAG'

If you don’t want to upload backups, you can skip setting the login and password. It’s recommended to save these variables in a local `.env` file and use `source .env` to load them before starting the server.

2. Download and start the Docker setup:
Get the docker-compose.yml file and launch the setup.
```bash
curl -o docker-compose.yml https://raw.githubusercontent.com/L3odr0id/minecraft-server-config/refs/heads/main/docker-compose.yml
docker compose up -d
```

## To copy the world backup from the image

1. Create container from image with dummy command
```bash
docker container create <image_id> echo "Hello, Docker!"
```

2. Copy from container
```bash
docker cp <container_id>:/data.tgz С:\local\path.tgz
```

## Update scoreboard for BlazeandCave's Advancements

```
/function bacap_rewards:update_score
```

## File Permissions

When running the container, directory permissions can sometimes block the server from writing data. The [official documentation](https://docker-minecraft-server.readthedocs.io/en/latest/variables/) notes that the server runs under a user with UID=1000 and GUID=1000.

Fix permissions:

```bash
source .env
sudo chown -R 1000:1000 "$MC_DATA_PATH" "$MC_BACKUPS_PATH"
sudo chmod -R u+rwX "$MC_DATA_PATH" "$MC_BACKUPS_PATH"
```

## Add your used to docker group

```bash
sudo usermod -aG docker $USER
```
