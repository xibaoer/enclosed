---
outline: deep
---

# Docker Installation

Enclosed can be easily installed and run using Docker. This method is recommended for users who want a quick and straightforward way to deploy their own instance of Enclosed with minimal setup.

## Prerequisites

Before you begin, ensure that you have Docker installed on your system. You can download and install Docker from the [official Docker website](https://www.docker.com/get-started).

## Basic Docker Run

To run Enclosed using Docker, you can use the following command:

From Docker Hub
```bash
docker run -d --name enclosed --restart unless-stopped -p 8787:8787 corentinth/enclosed
```

From GitHub Container Registry
```bash
docker run -d --name enclosed --restart unless-stopped -p 8787:8787 ghcr.io/corentin-th/enclosed
```

This command will download the Enclosed image and start the application, making it accessible at `http://localhost:8787`.

### Explanation of the Command

- `-d`: Runs the container in detached mode (in the background).
- `--name enclosed`: Names the container "enclosed" for easy identification.
- `--restart unless-stopped`: Configures the container to always restart unless it is explicitly stopped.
- `-p 8787:8787`: Maps port 8787 on your host to port 8787 in the container, making the application accessible on your local machine.
- `corentinth/enclosed` or `ghcr.io/corentin-th/enclosed`: Specifies the Docker image to use.

## Docker with Volume Persistence

To ensure that your notes and settings are preserved even if the container is stopped or removed, you can run Enclosed with volume persistence. Replace `/path/to/local/data` with the path to your local data directory:

From Docker Hub:
```bash
docker run -d --name enclosed --restart unless-stopped -p 8787:8787 -v /path/to/local/data:/app/.data --user $(id -u):$(id -g) corentinth/enclosed
```

From GitHub Container Registry:
```bash
docker run -d --name enclosed --restart unless-stopped -p 8787:8787 -v /path/to/local/data:/app/.data --user $(id -u):$(id -g) ghcr.io/corentin-th/enclosed
```

### Explanation of Additional Flags

- `-v /path/to/local/data:/app/.data`: Maps a local directory to the container's data directory, ensuring that data is stored persistently on your host machine.
- `--user $(id -u):$(id -g)`: Ensures that the container runs with the same user ID and group ID as your current user, preventing potential permission issues with the mounted volume.

## Managing the Docker Container

Once Enclosed is running in a Docker container, you can manage it using the following commands:

### Stopping the Container

To stop the Enclosed container, run:

```bash
docker stop enclosed
```

### Restarting the Container

To restart the container, use:

```bash
docker start enclosed
```

### Removing the Container

If you need to remove the container, stop it first and then remove it with:

```bash
docker stop enclosed
docker rm enclosed
```

## Updating Enclosed

To update your Enclosed instance to the latest version, first remove the existing container, pull the latest image, and then run the container again:

```bash
docker stop enclosed
docker rm enclosed

# From Docker Hub
docker pull corentinth/enclosed

# Or from GitHub Container Registry
docker pull ghcr.io/corentin-th/enclosed

# Run the container again
docker run -d --name enclosed --restart unless-stopped -p 8787:8787 -v /path/to/local/data:/app/.data --user $(id -u):$(id -g) corentinth/enclosed
```

This will ensure that you are using the latest version of Enclosed with all your previous data intact.

## Next Steps

Once you have Enclosed up and running, you can explore [configuration options](./configuration) to customize your instance further. For more advanced setups, consider using [Docker Compose](./docker-compose) to manage your Enclosed deployment.