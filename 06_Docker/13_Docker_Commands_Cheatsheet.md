# 📚 Docker Commands Cheat Sheet

This cheat sheet provides a quick reference to the most commonly used Docker commands. It is designed for rapid revision before interviews, certification exams, or day-to-day Docker usage.

---

# Table of Contents

- Docker Installation
- Docker Images
- Docker Containers
- Docker Registry
- Docker Networking
- Docker Volumes
- Docker Compose
- Docker System
- Docker BuildKit
- Docker Cleanup
- Interview Revision

---

# Docker Installation

| Command | Description |
|----------|-------------|
| `docker --version` | Display Docker version |
| `docker version` | Display Docker client and server versions |
| `docker info` | Show Docker Engine information |

---

# Docker Images

| Command | Description |
|----------|-------------|
| `docker images` | List downloaded images |
| `docker image ls` | List images (new syntax) |
| `docker pull IMAGE` | Download image |
| `docker push IMAGE` | Upload image to registry |
| `docker search IMAGE` | Search Docker Hub |
| `docker rmi IMAGE` | Remove image |
| `docker image prune` | Remove dangling images |
| `docker image prune -a` | Remove unused images |
| `docker inspect IMAGE` | Display image information |
| `docker history IMAGE` | Show image layers |
| `docker tag IMAGE NEW_TAG` | Tag image |
| `docker save IMAGE -o file.tar` | Export image |
| `docker load -i file.tar` | Import image |

---

# Docker Containers

| Command | Description |
|----------|-------------|
| `docker run IMAGE` | Create and start container |
| `docker run -d IMAGE` | Run in detached mode |
| `docker run -it IMAGE bash` | Interactive shell |
| `docker run --name NAME IMAGE` | Assign container name |
| `docker run -p HOST:CONTAINER IMAGE` | Publish ports |
| `docker run -v VOLUME:/PATH IMAGE` | Mount volume |
| `docker ps` | Running containers |
| `docker ps -a` | All containers |
| `docker stop CONTAINER` | Stop container |
| `docker start CONTAINER` | Start stopped container |
| `docker restart CONTAINER` | Restart container |
| `docker rm CONTAINER` | Remove container |
| `docker exec -it CONTAINER bash` | Execute shell |
| `docker attach CONTAINER` | Attach to running container |
| `docker logs CONTAINER` | View logs |
| `docker inspect CONTAINER` | Inspect container |
| `docker top CONTAINER` | Running processes |
| `docker stats` | Live resource usage |
| `docker rename OLD NEW` | Rename container |
| `docker pause CONTAINER` | Pause container |
| `docker unpause CONTAINER` | Resume container |
| `docker kill CONTAINER` | Force stop |

---

# Docker Registry

| Command | Description |
|----------|-------------|
| `docker login` | Login to registry |
| `docker logout` | Logout |
| `docker pull IMAGE` | Download image |
| `docker push IMAGE` | Upload image |
| `docker search IMAGE` | Search Docker Hub |
| `docker tag IMAGE TAG` | Create repository tag |

---

# Docker Networking

| Command | Description |
|----------|-------------|
| `docker network ls` | List networks |
| `docker network create NETWORK` | Create network |
| `docker network inspect NETWORK` | Inspect network |
| `docker network rm NETWORK` | Remove network |
| `docker network connect NETWORK CONTAINER` | Connect container |
| `docker network disconnect NETWORK CONTAINER` | Disconnect container |
| `docker network prune` | Remove unused networks |

---

# Docker Volumes

| Command | Description |
|----------|-------------|
| `docker volume create NAME` | Create volume |
| `docker volume ls` | List volumes |
| `docker volume inspect NAME` | Inspect volume |
| `docker volume rm NAME` | Remove volume |
| `docker volume prune` | Remove unused volumes |

---

# Docker Compose

| Command | Description |
|----------|-------------|
| `docker compose up` | Start services |
| `docker compose up -d` | Start in detached mode |
| `docker compose down` | Stop and remove services |
| `docker compose stop` | Stop services |
| `docker compose start` | Start services |
| `docker compose restart` | Restart services |
| `docker compose ps` | Running services |
| `docker compose logs` | View logs |
| `docker compose build` | Build images |
| `docker compose pull` | Pull latest images |
| `docker compose config` | Validate compose file |

---

# Docker BuildKit

| Command | Description |
|----------|-------------|
| `docker build .` | Build image |
| `docker build -t IMAGE .` | Build tagged image |
| `docker build --no-cache .` | Ignore cache |
| `docker buildx version` | Show Buildx version |
| `docker buildx ls` | List builders |
| `docker buildx create` | Create builder |
| `docker buildx inspect` | Inspect builder |
| `docker buildx build` | Advanced build |
| `docker buildx rm` | Remove builder |

---

# Docker System

| Command | Description |
|----------|-------------|
| `docker info` | Docker Engine information |
| `docker system df` | Docker disk usage |
| `docker system events` | Live Docker events |
| `docker system prune` | Remove unused resources |

---

# Docker Cleanup

## Remove Stopped Containers

```bash
docker container prune
```

---

## Remove Unused Images

```bash
docker image prune
```

---

## Remove Unused Volumes

```bash
docker volume prune
```

---

## Remove Unused Networks

```bash
docker network prune
```

---

## Remove Everything Unused

```bash
docker system prune
```

---

## Remove Everything Including Images

```bash
docker system prune -a
```

---

# Frequently Used Docker Run Examples

Run Nginx

```bash
docker run nginx
```

Run in Background

```bash
docker run -d nginx
```

Run with Port Mapping

```bash
docker run -d -p 8080:80 nginx
```

Run with Name

```bash
docker run --name web nginx
```

Run Interactive Ubuntu

```bash
docker run -it ubuntu bash
```

Run with Volume

```bash
docker run -v my-volume:/var/lib/mysql mysql
```

Run with Custom Network

```bash
docker run --network my-network nginx
```

---

# Interview Revision

## Image Commands

```text
docker images

docker pull

docker push

docker rmi

docker tag

docker history
```

---

## Container Commands

```text
docker run

docker ps

docker stop

docker start

docker restart

docker rm

docker exec

docker logs

docker inspect
```

---

## Network Commands

```text
docker network ls

docker network create

docker network inspect

docker network rm
```

---

## Volume Commands

```text
docker volume create

docker volume ls

docker volume inspect

docker volume rm
```

---

## Compose Commands

```text
docker compose up

docker compose down

docker compose logs

docker compose ps
```

---

## Build Commands

```text
docker build

docker buildx build

docker build --no-cache
```

---

# Docker Workflow (Quick Revision)

```text
Dockerfile
      │
docker build
      │
Docker Image
      │
docker push
      │
Registry
      │
docker pull
      │
docker run
      │
Container
      │
Application Running
```

---

# 30-Second Interview Revision

```text
docker run        → Create + Start Container

docker ps         → Running Containers

docker images     → List Images

docker pull       → Download Image

docker push       → Upload Image

docker build      → Build Image

docker exec       → Execute Command

docker logs       → View Logs

docker inspect    → Inspect Object

docker volume ls  → List Volumes

docker network ls → List Networks

docker compose up → Start Multi-container App

docker system df  → Disk Usage

docker system prune → Cleanup
```

---

# Summary

This cheat sheet consolidates the most frequently used Docker commands across image management, container operations, networking, storage, Docker Compose, BuildKit, and system maintenance. It serves as a quick-reference guide for daily development, troubleshooting, interview preparation, and certification revision.