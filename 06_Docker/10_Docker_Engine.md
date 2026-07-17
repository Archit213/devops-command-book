# ⚙️ Docker Engine

Docker Engine is the core runtime that enables you to build, run, and manage Docker containers. It consists of several components that work together to execute Docker commands and manage container lifecycles.

---

# Table of Contents

- [What is Docker Engine?](#what-is-docker-engine)
- [Docker Engine Components](#docker-engine-components)
- [Docker CLI](#docker-cli)
- [Docker Daemon](#docker-daemon)
- [Docker REST API](#docker-rest-api)
- [containerd](#containerd)
- [runc](#runc)
- [Docker Engine Workflow](#docker-engine-workflow)
- [Docker Engine Commands](#docker-engine-commands)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is Docker Engine?

Docker Engine is the software responsible for creating, running, and managing containers.

It acts as the bridge between the Docker CLI and the operating system.

Docker Engine is installed on:

- Linux
- Windows
- macOS (via Docker Desktop)

---

# Docker Engine Components

```text
              Docker CLI
                   │
                   ▼
            Docker REST API
                   │
                   ▼
            Docker Daemon
                   │
            ┌──────┴──────┐
            │             │
        containerd     Image Manager
            │
           runc
            │
      Linux Kernel
            │
      Running Containers
```

---

# Docker CLI

Docker CLI is the command-line tool users interact with.

Examples:

```bash
docker run
docker ps
docker build
docker pull
docker images
docker network ls
docker volume ls
```

The CLI itself never creates containers directly.

Instead, it communicates with the Docker Daemon.

---

# Docker Daemon

The Docker Daemon (`dockerd`) is the heart of Docker Engine.

Responsibilities:

- Build Images
- Run Containers
- Manage Networks
- Manage Volumes
- Pull Images
- Push Images
- Container Lifecycle

Daemon runs as a background service.

---

# Docker REST API

The Docker CLI communicates with the daemon using the Docker REST API.

Other applications can also communicate with Docker using the same API.

Examples:

- Docker Desktop
- Visual Studio Code
- GitHub Actions
- Jenkins
- Kubernetes
- CI/CD Pipelines

---

# containerd

containerd is Docker's container runtime.

Responsibilities:

- Container lifecycle
- Image management
- Snapshot management
- Storage management

Docker uses containerd internally to manage containers.

---

# runc

runc is the low-level runtime responsible for creating containers according to the OCI (Open Container Initiative) specification.

Flow:

```text
Docker CLI
      │
Docker Daemon
      │
containerd
      │
runc
      │
Linux Kernel
```

---

# Docker Engine Workflow

When you execute

```bash
docker run nginx
```

the following steps occur:

```text
Docker CLI
      │
Sends Request
      │
Docker Daemon
      │
Checks Local Images
      │
Pull Image (if needed)
      │
containerd
      │
runc
      │
Linux Kernel
      │
Container Starts
```

---

# Docker Engine Commands

| Command | Description |
|----------|-------------|
| `docker version` | Display client and server versions |
| `docker info` | Display Docker Engine information |
| `docker system info` | Detailed system information |
| `docker system df` | Docker disk usage |
| `docker system events` | Live Docker events |
| `docker system prune` | Remove unused Docker resources |

---

# Practical Examples

## Check Docker Version

```bash
docker version
```

Expected Output

```text
Client:
 Version: 28.x

Server:
 Engine:
 Version: 28.x
```

Use Case

Verify Docker client and server versions.

---

## Display Docker Information

```bash
docker info
```

Expected Output

```text
Containers: 5

Images: 12

Storage Driver: overlay2

Docker Root Dir:
/var/lib/docker
```

Use Case

Troubleshoot Docker Engine configuration.

---

## Check Disk Usage

```bash
docker system df
```

Expected Output

```text
Images

Containers

Volumes

Build Cache
```

Use Case

Identify Docker resources consuming disk space.

---

## View Docker Events

```bash
docker system events
```

Example Output

```text
container create

container start

container stop
```

Use Case

Monitor container lifecycle events in real time.

---

## Clean Up Docker

```bash
docker system prune
```

Expected Output

```text
Deleted Containers

Deleted Networks

Deleted Images

Deleted Build Cache
```

Use Case

Remove unused Docker resources and recover disk space.

---

# Common Mistakes

❌ Confusing Docker Engine with Docker Desktop.

❌ Stopping the Docker daemon and expecting containers to continue working.

❌ Forgetting that the Docker CLI depends on the daemon.

❌ Running unnecessary background containers that consume resources.

---

# Best Practices

- Keep Docker Engine updated.
- Monitor disk usage regularly.
- Remove unused images and containers.
- Use official Docker packages.
- Monitor daemon logs for troubleshooting.

---

# Quick Revision

```text
Docker CLI
      │
User Commands

Docker REST API
      │
Communication Layer

Docker Daemon
      │
Container Management

containerd
      │
Container Runtime

runc
      │
Creates Containers

Linux Kernel
      │
Runs Containers
```

---

# Interview Questions

## 1. What is Docker Engine?

Docker Engine is the core runtime responsible for building, running, and managing Docker containers.

---

## 2. What are the main components of Docker Engine?

- Docker CLI
- Docker Daemon
- Docker REST API
- containerd
- runc

---

## 3. What is the role of Docker Daemon?

It manages Docker objects such as images, containers, networks, and volumes.

---

## 4. What is containerd?

containerd is the container runtime that manages the complete lifecycle of containers.

---

## 5. What is runc?

runc is a lightweight runtime responsible for creating and running containers according to the OCI specification.

---

## 6. What does `docker system prune` do?

It removes unused:

- Containers
- Networks
- Images
- Build Cache

to free disk space.

---

# Summary

Docker Engine is the foundation of Docker. It combines the Docker CLI, Docker Daemon, REST API, containerd, and runc to build, manage, and run containers efficiently. Understanding Docker Engine is essential for troubleshooting, optimizing performance, and preparing for Docker and DevOps interviews.