# 📦 Docker Containers

A **Docker Container** is a lightweight, isolated runtime instance of a Docker Image. Containers package an application along with its dependencies, libraries, and runtime environment, ensuring consistent behavior across development, testing, and production environments.

---

# Table of Contents

- [What is a Container?](#what-is-a-container)
- [Container Lifecycle](#container-lifecycle)
- [Container States](#container-states)
- [Docker Container Commands](#docker-container-commands)
- [Container Workflow](#container-workflow)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is a Container?

A Docker Container is a running instance of a Docker Image.

An image is a blueprint.

A container is the running application created from that blueprint.

Example:

```text
Docker Image
      │
      ├── Container 1
      ├── Container 2
      ├── Container 3
      └── Container 4
```

Multiple containers can be created from the same image.

Each container is isolated and has its own:

- Filesystem
- Network Interface
- Process Space
- Environment Variables

---

# Container Lifecycle

Every container goes through the following stages:

```text
Docker Image
      │
docker run
      │
Created
      │
Started
      │
Running
      │
Stopped
      │
Removed
```

---

# Container States

| State | Description |
|---------|-------------|
| Created | Container has been created but not started |
| Running | Container is actively executing |
| Paused | Processes are temporarily suspended |
| Restarting | Docker is restarting the container |
| Exited | Container has stopped |
| Dead | Container cannot be recovered |

---

# Docker Container Commands

| Command | Description |
|----------|-------------|
| `docker run IMAGE` | Create and start a container |
| `docker run --name container_name IMAGE` | |Create a named container with the existing image|
| `docker run -d IMAGE` | Run container in detached mode |
| `docker run -it IMAGE` | Interactive terminal |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers |
| `docker stop CONTAINER` | Stop a running container |
| `docker start CONTAINER` | Start an existing container |
| `docker restart CONTAINER` | Restart container |
| `docker rm CONTAINER` | Remove container |
| `docker exec -it CONTAINER bash` | Execute command inside container |
| `docker attach CONTAINER` | Attach to running container |
| `docker logs CONTAINER` | View container logs |
| `docker inspect CONTAINER` | Detailed container information |
| `docker top CONTAINER` | Running processes inside container |
| `docker stats` | Live resource usage |
| `docker rename OLD NEW` | Rename a container |
| `docker pause CONTAINER` | Pause processes |
| `docker unpause CONTAINER` | Resume paused container |
| `docker kill CONTAINER` | Forcefully stop a container |

---

# Container Workflow

```text
docker pull nginx
        │
        ▼
docker run nginx
        │
        ▼
Container Created
        │
        ▼
Application Running
        │
        ▼
docker stop
        │
        ▼
Stopped
        │
        ▼
docker start
        │
        ▼
Running Again
```

---

# Practical Examples

## 1. Create a Container

Purpose

Create and immediately start a container.

Syntax

```bash
docker run nginx
```

Example

```bash
docker run nginx
```

Expected Output

```text
Unable to find image 'nginx:latest' locally

Pulling from library/nginx

Status: Downloaded newer image
```

Use Case

Deploy a temporary Nginx server for testing.

---

## 2. Run in Detached Mode

Purpose

Run container in the background.

Syntax

```bash
docker run -d IMAGE
```

Example

```bash
docker run -d nginx
```

Expected Output

```text
a7b18e47fcaf54f8d97c0b2f...
```

Use Case

Running production web servers without occupying the terminal.

---

## 3. Interactive Container

Purpose

Access a shell inside the container.

Syntax

```bash
docker run -it ubuntu bash
```

Example

```bash
docker run -it ubuntu bash
```

Expected Output

```text
root@8c5d3b9:/#
```

Use Case

Troubleshooting or testing Linux commands inside a container.

---

## 4. List Running Containers

Syntax

```bash
docker ps
```

Expected Output

```text
CONTAINER ID

IMAGE

STATUS

PORTS

NAMES
```

Use Case

Check active containers before deployment.

---

## 5. List All Containers

```bash
docker ps -a
```

Shows:

- Running
- Stopped
- Exited

containers.

---

## 6. Stop Container

```bash
docker stop nginx-container
```

Expected Output

```text
nginx-container
```

Use Case

Gracefully stop an application before maintenance.

---

## 7. Start Existing Container

```bash
docker start nginx-container
```

Expected Output

```text
nginx-container
```

Use Case

Restart an application without creating a new container.

---

## 8. Restart Container

```bash
docker restart nginx-container
```

Use Case

Reload an application after configuration changes.

---

## 9. Remove Container

```bash
docker rm nginx-container
```

Expected Output

```text
nginx-container
```

Use Case

Clean up unused containers.

---

## 10. Execute Commands

```bash
docker exec -it nginx-container bash
```

Expected Output

```text
root@container:/#
```

Use Case

Debug applications running inside containers.

---

## 11. Attach to Container

```bash
docker attach nginx-container
```

Use Case

Reconnect to the primary process of a running container.

---

## 12. View Logs

```bash
docker logs nginx-container
```

Expected Output

```text
2026-07-17 12:30:10 GET /
```

Use Case

Troubleshoot application startup failures.

---

## 13. Inspect Container

```bash
docker inspect nginx-container
```

Expected Output

```json
{
  "Id": "...",
  "State": {
    "Running": true
  },
  "NetworkSettings": {}
}
```

Use Case

Retrieve networking, volumes, IP address, and configuration details.

---

## 14. Running Processes

```bash
docker top nginx-container
```

Expected Output

```text
PID USER COMMAND
```

Use Case

View active processes inside a container.

---

## 15. Resource Usage

```bash
docker stats
```

Expected Output

```text
CONTAINER ID

CPU %

MEM USAGE

NET I/O
```

Use Case

Monitor CPU and memory usage in real time.

---

## 16. Rename Container

```bash
docker rename old-name new-name
```

Use Case

Assign meaningful names to containers.

---

## 17. Pause Container

```bash
docker pause nginx-container
```

Suspends all processes without stopping the container.

---

## 18. Resume Container

```bash
docker unpause nginx-container
```

Resumes execution of paused processes.

---

## 19. Kill Container

```bash
docker kill nginx-container
```

Immediately terminates the container.

Unlike `docker stop`, this does not wait for graceful shutdown.

---

# Common Mistakes

❌ Forgetting `-d` when running long-lived services.

❌ Removing running containers without stopping them.

❌ Using `docker kill` instead of `docker stop`.

❌ Confusing `docker exec` with `docker attach`.

❌ Creating multiple containers unnecessarily instead of restarting an existing one.

---

# Best Practices

- Assign meaningful container names using `--name`.
- Stop containers gracefully using `docker stop`.
- Remove unused containers regularly.
- Use detached mode for production services.
- Use `docker exec` instead of `docker attach` for troubleshooting.
- Monitor container logs and resource usage.

---

# Quick Revision

```text
docker run        → Create + Start

docker ps         → Running Containers

docker ps -a      → All Containers

docker stop       → Stop

docker start      → Start Existing

docker restart    → Restart

docker exec       → Execute Command

docker attach     → Attach Terminal

docker logs       → View Logs

docker inspect    → Detailed Information

docker stats      → Resource Usage

docker rm         → Remove Container
```

---

# Interview Questions

### 1. What is a Docker Container?

A lightweight runtime instance of a Docker Image.

---

### 2. Difference between Image and Container?

An Image is a read-only template, whereas a Container is a running instance of that image.

---

### 3. Difference between `docker run` and `docker start`?

- `docker run` creates a new container and starts it.
- `docker start` starts an already existing stopped container.

---

### 4. Difference between `docker exec` and `docker attach`?

- `docker exec` starts a new process inside a running container.
- `docker attach` connects to the container's primary process.

---

### 5. Difference between `docker stop` and `docker kill`?

- `docker stop` performs a graceful shutdown.
- `docker kill` immediately terminates the container.

---

# Summary

Docker Containers are isolated runtime environments created from Docker Images. They provide portability, consistency, and efficient resource utilization by sharing the host operating system kernel. Mastering the container lifecycle and management commands is essential for every DevOps engineer.