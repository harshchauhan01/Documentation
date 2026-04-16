# Docker Guide

## What Docker Is
Docker is a platform for building, shipping, and running applications inside lightweight, isolated environments called containers.

### Core Definitions
- Image: A read-only template that contains an application, its dependencies, and configuration.
- Container: A running instance of an image.
- Dockerfile: A text file that defines how to build a Docker image.
- Registry: A storage service for Docker images, such as Docker Hub.
- Volume: Persistent storage that survives container deletion.
- Network: A virtual network that allows containers to communicate.
- Compose: A tool for defining and running multi-container applications with a YAML file.

## Installation

### Windows Installation
1. Check that virtualization is enabled in BIOS or UEFI.
2. Enable WSL 2 if you plan to use Docker Desktop with the WSL backend.
3. Download Docker Desktop from the official Docker website.
4. Run the installer and follow the setup prompts.
5. Restart the system if required.
6. Open Docker Desktop and confirm it starts successfully.
7. Verify installation from a terminal:

```powershell
docker --version
docker compose version
```

### Linux Installation Example
The exact package commands depend on your distribution. On Ubuntu, installation commonly follows this pattern:

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
	"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
	$(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
	sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

```
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

After installation, test Docker with:

```bash
sudo docker run hello-world
```

```bash
sudo usermod -aG docker $USER
```
This command adds the current user ($USER) to the docker group, allowing you to run Docker commands without needing sudo.

## Basic Docker Concepts

### 1. Docker Client and Daemon
- Docker Client: The command-line tool you use to send commands.
- Docker Daemon: The background service that builds, runs, and manages containers.

### 2. Image Layers
Docker images are built in layers. Each instruction in a Dockerfile usually creates a new layer, which helps with caching and reuse.

### 3. Container Lifecycle
Containers can be created, started, stopped, paused, restarted, and removed.

## Essential Commands

### Check Docker Version
```bash
docker --version
docker version
```

### Display System Information
```bash
docker info
```

### Search for Images
```bash
docker search nginx
```

### Download an Image
```bash
docker pull ubuntu:latest
docker pull nginx:alpine
```

### List Images
```bash
docker images
docker image ls
```

### Run a Container
```bash
docker run hello-world
docker run -it ubuntu bash
docker run -d -p 8080:80 nginx
```

### Run with Common Options
- `-d`: Run in detached mode.
- `-it`: Open an interactive terminal.
- `--name`: Assign a container name.
- `-p`: Publish a port from container to host.
- `-v`: Mount a volume or folder.
- `--rm`: Remove the container automatically after exit.

Examples:

```bash
docker run --name my-nginx -d -p 8080:80 nginx
docker run --rm -it ubuntu bash
docker run -v mydata:/data alpine
```

### List Running Containers
```bash
docker ps
docker container ls
```

### List All Containers
```bash
docker ps -a
docker container ls -a
```

### Stop a Container
```bash
docker stop my-nginx
```

### Start a Container
```bash
docker start my-nginx
```

### Restart a Container
```bash
docker restart my-nginx
```

### Remove a Container
```bash
docker rm my-nginx
docker rm -f my-nginx
```

### Remove an Image
```bash
docker rmi nginx:alpine
```

## Working With Container Logs and Processes

### View Logs
```bash
docker logs my-nginx
docker logs -f my-nginx
```

### Inspect a Container
```bash
docker inspect my-nginx
```

### Show Running Processes Inside a Container
```bash
docker top my-nginx
```

### Execute a Command Inside a Running Container
```bash
docker exec -it my-nginx bash
docker exec my-nginx ls /usr/share/nginx/html
```

## Dockerfile Basics

### What a Dockerfile Does
A Dockerfile defines the steps needed to build a Docker image in a repeatable way.

### Common Dockerfile Instructions
- `FROM`: Base image.
- `WORKDIR`: Sets the working directory.
- `COPY`: Copies files into the image.
- `RUN`: Executes build-time commands.
- `EXPOSE`: Documents the port used by the container.
- `CMD`: Default command when the container starts.
- `ENTRYPOINT`: Fixed startup command.
- `ENV`: Defines environment variables.

### Example Dockerfile
```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

### Build an Image
```bash
docker build -t my-app:1.0 .
```

### Build With a Dockerfile Name
```bash
docker build -f Dockerfile.dev -t my-app-dev .
```

### Tag an Image
```bash
docker tag my-app:1.0 myrepo/my-app:1.0
```

### Push an Image to a Registry
```bash
docker login
docker push myrepo/my-app:1.0
```

### Pull an Image From a Registry
```bash
docker pull myrepo/my-app:1.0
```

## Volumes and Storage

### Why Volumes Matter
Containers are ephemeral. Volumes keep data even when containers are deleted.

### Create a Volume
```bash
docker volume create my-volume
```

### List Volumes
```bash
docker volume ls
```

### Inspect a Volume
```bash
docker volume inspect my-volume
```

### Use a Volume
```bash
docker run -d --name db -v my-volume:/var/lib/mysql mysql:8
```

### Remove a Volume
```bash
docker volume rm my-volume
```

## Networks

### Why Docker Networks Are Used
Networks let containers communicate with each other and with the host in a controlled way.

### Create a Network
```bash
docker network create my-network
```

### List Networks
```bash
docker network ls
```

### Inspect a Network
```bash
docker network inspect my-network
```

### Run Containers on the Same Network
```bash
docker run -d --name app --network my-network nginx
docker run -it --rm --network my-network alpine sh
```

### Remove a Network
```bash
docker network rm my-network
```

## Docker Compose

### What Docker Compose Does
Docker Compose manages multi-container applications using a single YAML file.

### Example compose.yaml
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: secret
```

### Start Services
```bash
docker compose up
docker compose up -d
```

### Stop Services
```bash
docker compose down
```

### Rebuild and Start
```bash
docker compose up --build -d
```

### View Compose Logs
```bash
docker compose logs
docker compose logs -f
```

### List Compose Services
```bash
docker compose ps
```

## Advanced Commands

### Resource Usage
```bash
docker stats
```

### Save an Image to a File
```bash
docker save -o ubuntu.tar ubuntu:latest
```

### Load an Image From a File
```bash
docker load -i ubuntu.tar
```

### Export a Container File System
```bash
docker export -o container.tar my-container
```

### Import a Tar Archive as an Image
```bash
docker import container.tar my-image:latest
```

### Clean Up Unused Resources
```bash
docker system prune
docker system prune -a
docker volume prune
docker network prune
```

### Remove All Stopped Containers
```bash
docker container prune
```

### Remove Dangling Images
```bash
docker image prune
```

### Remove Unused Build Cache
```bash
docker builder prune
```

## Helpful Patterns

### Interactive Shell in a Container
```bash
docker run -it --rm ubuntu bash
```

### Mount Current Directory Into a Container
```bash
docker run -it --rm -v ${PWD}:/app -w /app node:20-alpine sh
```

### Map Ports
```bash
docker run -d -p 3000:3000 my-app
```

### Pass Environment Variables
```bash
docker run -e NODE_ENV=production my-app
```

### Set a Restart Policy
```bash
docker run -d --restart unless-stopped nginx
```

## Troubleshooting Commands

### Check Whether Docker Is Running
```bash
docker info
```

### Review Container Exit Status
```bash
docker ps -a
docker inspect my-container
```

### Follow Logs for Errors
```bash
docker logs -f my-container
```

### Enter a Container for Debugging
```bash
docker exec -it my-container sh
```

## Practical Workflow
1. Write a Dockerfile.
2. Build an image with `docker build`.
3. Run the container with `docker run`.
4. Inspect logs with `docker logs`.
5. Update the app and rebuild the image.
6. Use volumes and networks when the app needs persistent data or service-to-service communication.

## Quick Command Reference

```bash
docker --version
docker info
docker pull IMAGE
docker images
docker run IMAGE
docker ps
docker ps -a
docker stop CONTAINER
docker start CONTAINER
docker restart CONTAINER
docker rm CONTAINER
docker rmi IMAGE
docker logs CONTAINER
docker exec -it CONTAINER sh
docker build -t NAME .
docker tag SOURCE TARGET
docker push IMAGE
docker volume ls
docker network ls
docker compose up -d
docker compose down
docker system prune
```

## Summary
Docker makes application delivery repeatable by packaging software and its dependencies into containers. The most important daily commands are `docker pull`, `docker run`, `docker ps`, `docker logs`, `docker exec`, `docker build`, and `docker compose up`.
