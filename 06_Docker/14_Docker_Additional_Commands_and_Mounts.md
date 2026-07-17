# 🧩 Docker Additional Commands and Storage Mounts

This supplemental guide collects the Docker commands and concepts that were not fully covered in the earlier topic files. It focuses on creating containers from existing images, storage mounts, lifecycle management, logging, inspection, networking, and image-management commands.

---

# Table of Contents

- [Create Containers from Existing Images](#create-containers-from-existing-images)
- [Storage Mount Types](#storage-mount-types)
- [Additional Container Lifecycle Commands](#additional-container-lifecycle-commands)
- [Container Logging Commands](#container-logging-commands)
- [Docker Inspect Commands](#docker-inspect-commands)
- [Additional Networking Commands](#additional-networking-commands)
- [Additional Image Commands](#additional-image-commands)
- [Volume Creation and Mount Workflow](#volume-creation-and-mount-workflow)
- [Quick Revision](#quick-revision)

---

# Create Containers from Existing Images

The `docker run` command creates a new container from an existing Docker image and starts it immediately.

General syntax:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

If the image is not available locally, Docker automatically tries to pull it from the configured registry.

## Command Reference

| Command | Description |
|----------|-------------|
| `docker run ubuntu` | Create and start a container from the Ubuntu image |
| `docker run --name ubuntu-container ubuntu` | Create a container with a custom name |
| `docker run -d nginx` | Create and run an Nginx container in detached mode |
| `docker run -it ubuntu bash` | Create an interactive Ubuntu container and open Bash |
| `docker run -d -p 8080:80 nginx` | Create a container and map host port 8080 to container port 80 |
| `docker run -e APP_COLOR=blue kodekloud/simple-webapp` | Create a container with an environment variable |
| `docker run --restart unless-stopped nginx` | Create a container with an automatic restart policy |
| `docker run --cpus="2" nginx` | Limit the container to two CPUs |
| `docker run -m 512m nginx` | Limit container memory to 512 MB |

---

## Create a Basic Container

### How and Where to Use

Use this when you want to create a container directly from an existing image using its default startup command.

### Example

```bash
docker run ubuntu
```

### Expected Output

```text
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
Status: Downloaded newer image for ubuntu:latest
```

> The Ubuntu container may exit immediately because the image does not start a long-running foreground process by default.

---

## Create a Named Container

### How and Where to Use

Use a meaningful container name to make administration, troubleshooting, and automation easier.

### Example

```bash
docker run --name ubuntu-container ubuntu
```

### Expected Output

```text
Unable to find image 'ubuntu:latest' locally
Status: Image is up to date for ubuntu:latest
```

Verify the container:

```bash
docker ps -a
```

```text
CONTAINER ID   IMAGE    STATUS                     NAMES
8a72f6a210a1   ubuntu   Exited (0) 5 seconds ago   ubuntu-container
```

---

## Create a Detached Container

### How and Where to Use

Detached mode is used for long-running services such as web servers, databases, and APIs.

### Example

```bash
docker run -d nginx
```

### Expected Output

```text
72df948ad84e93f8be75be0f8f2a92409bc5a66b5d8b5f5d93fc6b5bf0b1b9e8
```

The returned value is the container ID.

---

## Create an Interactive Container

### How and Where to Use

Use interactive mode when you need a terminal inside the container for testing, learning, or troubleshooting.

### Example

```bash
docker run -it ubuntu bash
```

### Expected Output

```text
root@5c804c9c7f2f:/#
```

Exit the container shell:

```bash
exit
```

---

## Create a Container with Port Mapping

### How and Where to Use

Use port mapping to expose a service running inside a container to the host or external users.

### Example

```bash
docker run -d --name web -p 8080:80 nginx
```

### Expected Output

```text
a82eb6481cd35a7ea2c2124cb3cdb4aa0882d2af8ec0f81e3697d5f61370a91b
```

Access the service at:

```text
http://localhost:8080
```

Mapping:

```text
Host Port 8080
      │
      ▼
Container Port 80
```

---

## Create a Container with Environment Variables

### How and Where to Use

Environment variables are commonly used to provide runtime configuration without modifying an image.

### Example

```bash
docker run -d \
  --name blue-app \
  -e APP_COLOR=blue \
  -p 8080:8080 \
  kodekloud/simple-webapp
```

### Expected Output

```text
f0e3ed45d2b6c521f208573d3ce76a47c1ee21452983b02166f243a4cd0c128e
```

Verify the variable:

```bash
docker exec blue-app printenv APP_COLOR
```

```text
blue
```

---

## Create a Container with a Restart Policy

### How and Where to Use

Restart policies are useful for production services that should restart after a crash or Docker daemon restart.

### Example

```bash
docker run -d \
  --name web \
  --restart unless-stopped \
  nginx
```

### Expected Output

```text
ce81a7f9f3083aa3ec59a28189a57d42f3b7199255f6635ae4c1899db9e3f434
```

Common restart policies:

| Policy | Behaviour |
|--------|-----------|
| `no` | Do not restart automatically |
| `on-failure` | Restart only when the process exits with an error |
| `always` | Always restart the container |
| `unless-stopped` | Restart automatically unless it was manually stopped |

---

## Create a Container with a CPU Limit

### How and Where to Use

Use CPU limits to prevent a container from consuming excessive host resources.

### Example

```bash
docker run -d \
  --name cpu-limited-app \
  --cpus="2" \
  nginx
```

### Expected Output

```text
0d77a368ef64811d83dfa93bbb908743c12e31c574681a19c781a6be718f93b0
```

Verify:

```bash
docker inspect cpu-limited-app --format '{{.HostConfig.NanoCpus}}'
```

```text
2000000000
```

---

## Create a Container with a Memory Limit

### How and Where to Use

Use memory limits to protect the host from a container consuming all available RAM.

### Example

```bash
docker run -d \
  --name memory-limited-app \
  -m 512m \
  nginx
```

### Expected Output

```text
0ab759a4455805f69363a641a171336bf034f59e7f25e9956f4e59317246662c
```

Verify:

```bash
docker inspect memory-limited-app --format '{{.HostConfig.Memory}}'
```

```text
536870912
```

---

# Storage Mount Types

Docker supports three primary storage mount types:

| Mount Type | Description | Typical Use |
|------------|-------------|-------------|
| Volume | Docker-managed persistent storage | Databases and production workloads |
| Bind mount | Maps a specific host path into a container | Development and configuration files |
| tmpfs | Stores data in host memory only | Temporary or sensitive data |

---

## Volume Mount

A named volume is managed by Docker and persists independently of the container lifecycle.

### Create the Volume

```bash
docker volume create mysql-data
```

### Expected Output

```text
mysql-data
```

### Mount the Volume with `-v`

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=StrongPassword123 \
  -v mysql-data:/var/lib/mysql \
  mysql:8
```

### Expected Output

```text
a88a269a12c1e8600a38c2bbde9667a6c89dbccac38a3ae470ff6cb95034c047
```

### How and Where to Use

Use named volumes for persistent database data, Jenkins home directories, monitoring data, or application uploads.

---

## Bind Mount

A bind mount maps an existing host file or directory directly into a container.

### Example

```bash
docker run -d \
  --name node-app \
  -v /home/aru/app:/app \
  node:20
```

### Expected Output

```text
47a5e61a442ad359828ce691246d91b83e54df7ec15ea511719bb9b36f6507a4
```

### How and Where to Use

Bind mounts are useful during development because source-code changes on the host become immediately available inside the container.

> The host path must exist and should use an absolute path.

---

## tmpfs Mount

A tmpfs mount stores data only in memory. It is removed when the container stops.

### Example using `--tmpfs`

```bash
docker run -d \
  --name cache-app \
  --tmpfs /app/cache \
  nginx
```

### Expected Output

```text
6ab0d1eb928233f71c029e8e5f062104e04adb76d250ff9ce4dd4b24cc6da9e7
```

### How and Where to Use

Use tmpfs for:

- Temporary cache files
- Sensitive temporary information
- High-speed non-persistent data

---

## Modern `--mount` Syntax

The `--mount` syntax is more explicit and readable than `-v`.

### Named Volume

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=StrongPassword123 \
  --mount type=volume,source=mysql-data,target=/var/lib/mysql \
  mysql:8
```

### Bind Mount

```bash
docker run -d \
  --name web-app \
  --mount type=bind,source=/home/aru/app,target=/usr/share/nginx/html \
  nginx
```

### tmpfs Mount

```bash
docker run -d \
  --name temp-app \
  --mount type=tmpfs,target=/app/cache \
  nginx
```

### Recommended Use

Prefer `--mount` in documentation, automation, and production scripts because each option is clearly named.

---

# Additional Container Lifecycle Commands

## Command Reference

| Command | Description |
|----------|-------------|
| `docker create IMAGE` | Create a container without starting it |
| `docker start CONTAINER` | Start an existing stopped container |
| `docker wait CONTAINER` | Wait for a container to stop and print its exit code |
| `docker cp SOURCE DESTINATION` | Copy files between the host and a container |
| `docker export CONTAINER` | Export a container filesystem as a tar archive |
| `docker import FILE` | Create an image from an exported filesystem archive |

---

## Create without Starting

```bash
docker create --name sleeping-container ubuntu sleep 1000
```

### Expected Output

```text
1176e4f08ac92c0fe134ab6b22ac448e08d6ff5aeb5e58394fd9cadc8a418659
```

Start it later:

```bash
docker start sleeping-container
```

```text
sleeping-container
```

---

## Wait for a Container to Exit

```bash
docker run -d --name short-job ubuntu sleep 5
docker wait short-job
```

### Expected Output

```text
0
```

`0` is the successful exit code returned by the container.

---

## Copy a File from Host to Container

```bash
docker cp ./app.conf web:/etc/app/app.conf
```

### Expected Output

```text
Successfully copied 2.05kB to web:/etc/app/app.conf
```

Copy from container to host:

```bash
docker cp web:/var/log/nginx/access.log ./access.log
```

---

## Export a Container Filesystem

```bash
docker export web -o web-filesystem.tar
```

### Expected Output

```text
$
```

No output generally indicates success.

---

## Import a Filesystem as an Image

```bash
docker import web-filesystem.tar web-filesystem:v1
```

### Expected Output

```text
sha256:565c9e7812bca993f993ea9ce68a39531e3bdd473140f84c892451df337b4d99
```

> `docker export` and `docker import` do not preserve image history, metadata, or volumes. Use `docker save` and `docker load` when you need to preserve a complete Docker image.

---

# Container Logging Commands

## Command Reference

| Command | Description |
|----------|-------------|
| `docker logs CONTAINER` | Display container logs |
| `docker logs -f CONTAINER` | Follow logs continuously |
| `docker logs --tail 100 CONTAINER` | Show only the last 100 log lines |
| `docker logs --since 30m CONTAINER` | Show logs generated during the last 30 minutes |
| `docker logs -t CONTAINER` | Include timestamps |

---

## Follow Logs Continuously

```bash
docker logs -f nginx-container
```

### Expected Output

```text
172.17.0.1 - - [17/Jul/2026:08:10:03 +0000] "GET / HTTP/1.1" 200 615
172.17.0.1 - - [17/Jul/2026:08:10:06 +0000] "GET /favicon.ico HTTP/1.1" 404 153
```

Stop following with `Ctrl+C`.

---

## Display the Last 100 Lines

```bash
docker logs --tail 100 nginx-container
```

### Expected Output

```text
2026/07/17 08:15:01 [notice] nginx started
2026/07/17 08:15:03 [info] request completed
```

---

## Display Recent Logs

```bash
docker logs --since 30m nginx-container
```

### Expected Output

```text
2026/07/17 08:30:20 [info] GET /health 200
2026/07/17 08:31:10 [info] GET /api/status 200
```

---

# Docker Inspect Commands

`docker inspect` returns detailed JSON configuration and runtime information.

## Command Reference

| Command | Description |
|----------|-------------|
| `docker inspect OBJECT` | Inspect any supported Docker object |
| `docker container inspect CONTAINER` | Inspect a container |
| `docker image inspect IMAGE` | Inspect an image |
| `docker volume inspect VOLUME` | Inspect a volume |
| `docker network inspect NETWORK` | Inspect a network |

---

## Inspect a Container

```bash
docker container inspect nginx-container
```

### Expected Output

```json
[
  {
    "Id": "72df948ad84e...",
    "State": {
      "Status": "running",
      "Running": true
    },
    "NetworkSettings": {
      "IPAddress": "172.17.0.2"
    }
  }
]
```

Retrieve only the IP address:

```bash
docker inspect \
  --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' \
  nginx-container
```

```text
172.17.0.2
```

---

## Inspect an Image

```bash
docker image inspect nginx:latest
```

### Expected Output

```json
[
  {
    "RepoTags": [
      "nginx:latest"
    ],
    "Architecture": "amd64",
    "Os": "linux"
  }
]
```

---

## Inspect a Volume

```bash
docker volume inspect mysql-data
```

### Expected Output

```json
[
  {
    "Name": "mysql-data",
    "Driver": "local",
    "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data"
  }
]
```

---

## Inspect a Network

```bash
docker network inspect bridge
```

### Expected Output

```json
[
  {
    "Name": "bridge",
    "Driver": "bridge",
    "IPAM": {
      "Config": [
        {
          "Subnet": "172.17.0.0/16",
          "Gateway": "172.17.0.1"
        }
      ]
    }
  }
]
```

---

# Additional Networking Commands

## Display Published Ports

```bash
docker port nginx-container
```

### Expected Output

```text
80/tcp -> 0.0.0.0:8080
80/tcp -> [::]:8080
```

### How and Where to Use

Use this command when troubleshooting whether a container port was correctly published to the host.

---

## Inspect the Default Bridge Network

```bash
docker network inspect bridge
```

Use this command to check:

- Subnet
- Gateway
- Connected containers
- Container IP addresses
- Network driver

---

# Additional Image Commands

Docker supports both general and object-specific command syntax.

| General Syntax | Object-specific Syntax |
|----------------|------------------------|
| `docker inspect nginx` | `docker image inspect nginx` |
| `docker history nginx` | `docker image history nginx` |

---

## Inspect an Image

```bash
docker image inspect nginx
```

### Expected Output

```json
[
  {
    "Id": "sha256:...",
    "RepoTags": [
      "nginx:latest"
    ]
  }
]
```

---

## View Image Layer History

```bash
docker image history nginx
```

### Expected Output

```text
IMAGE          CREATED       CREATED BY                                      SIZE
1e5f3c5b981a   2 weeks ago   CMD ["nginx" "-g" "daemon off;"]                0B
<missing>      2 weeks ago   COPY file:... /etc/nginx/nginx.conf             4.62kB
<missing>      2 weeks ago   RUN /bin/sh -c apt-get update ...                52.1MB
```

### How and Where to Use

Use image history to understand image layers, identify large layers, and improve Dockerfile efficiency.

---

# Volume Creation and Mount Workflow

```text
Create Volume
docker volume create mysql-data
          │
          ▼
Run Container
docker run -v mysql-data:/var/lib/mysql mysql:8
          │
          ▼
Application Writes Data
          │
          ▼
Docker Volume on Host
/var/lib/docker/volumes/mysql-data/_data
          │
          ▼
Container Removed
          │
          ▼
Data Still Exists
```

## Complete Example

Create a named volume:

```bash
docker volume create mysql-data
```

Create a MySQL container using the volume:

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=StrongPassword123 \
  -v mysql-data:/var/lib/mysql \
  mysql:8
```

Verify the mount:

```bash
docker inspect mysql-db \
  --format '{{json .Mounts}}'
```

### Expected Output

```json
[{"Type":"volume","Name":"mysql-data","Source":"/var/lib/docker/volumes/mysql-data/_data","Destination":"/var/lib/mysql","Driver":"local","Mode":"z","RW":true}]
```

Remove the container:

```bash
docker rm -f mysql-db
```

The volume still exists:

```bash
docker volume ls
```

```text
DRIVER    VOLUME NAME
local     mysql-data
```

---

# Quick Revision

```text
docker run IMAGE
    → Create and start a container from an image

docker run --name NAME IMAGE
    → Create a named container

docker run -d IMAGE
    → Detached mode

docker run -it IMAGE bash
    → Interactive shell

docker run -p HOST:CONTAINER IMAGE
    → Publish a container port

docker run -e KEY=value IMAGE
    → Pass an environment variable

docker run -v VOLUME:PATH IMAGE
    → Mount a volume

docker run --mount ...
    → Explicit modern mount syntax

docker create IMAGE
    → Create without starting

docker start CONTAINER
    → Start an existing container

docker cp
    → Copy files between host and container

docker logs -f
    → Follow logs continuously

docker inspect
    → Detailed object information

docker port
    → Show published ports

docker image history
    → Display image layers
```

---

# Summary

This guide adds the container-creation, storage-mount, lifecycle, logging, inspection, networking, and image commands that were not fully detailed in the earlier files. It can be used as a standalone supplemental chapter or merged later into the relevant Docker topic files.
