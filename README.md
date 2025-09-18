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
curl -o docker-compose.yml https://raw.githubusercontent.com/L3odr0id/minecraft-server-config/refs/heads/main/docker-compose.yml && docker compose up -d
```
