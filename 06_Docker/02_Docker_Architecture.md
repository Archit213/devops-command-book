# 🏗️ Docker Architecture

Docker Architecture defines how Docker works internally to build, manage, and run containers. Understanding the architecture is essential for troubleshooting, optimizing deployments, and preparing for Docker interviews.

---

# Table of Contents

- [Overview](#overview)
- [Docker Architecture Components](#docker-architecture-components)
- [Docker Engine](#docker-engine)
- [Docker Daemon (dockerd)](#docker-daemon-dockerd)
- [Docker CLI](#docker-cli)
- [Docker REST API](#docker-rest-api)
- [Container Runtime](#container-runtime)
- [How Docker Works Internally](#how-docker-works-internally)
- [Linux Kernel Sharing](#linux-kernel-sharing)
- [Docker Editions](#docker-editions)
- [Docker Subscription Plans](#docker-subscription-plans)
- [Architecture Diagram](#architecture-diagram)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# Overview

Docker follows a **Client-Server Architecture**.

When you execute a Docker command such as:

```bash
docker run nginx
```

the Docker CLI does **not** create the container directly.

Instead, it sends a request to the Docker Daemon, which performs all the required operations.

---

# Docker Architecture Components

```text
                 Docker Client
                  (Docker CLI)
                       │
             Docker REST API
                       │
                Docker Daemon
                  (dockerd)
                       │
              Container Runtime
                (containerd)
                       │
                     runc
                       │
                  Linux Kernel
                       │
                 Running Containers
```

---

# Docker Engine

Docker Engine is the core software responsible for running Docker.

It consists of:

- Docker CLI
- Docker Daemon
- Docker REST API

Docker Engine is installed on Linux, Windows, or macOS and manages the complete lifecycle of containers.

---

# Docker Daemon (dockerd)

The **Docker Daemon** is a background service.

It is responsible for managing:

- Images
- Containers
- Networks
- Volumes
- Build operations

Whenever you execute a Docker command, the daemon performs the requested operation.

Example:

```bash
docker run nginx
```

Flow:

```text
Docker CLI
      │
      ▼
Docker Daemon
      │
Downloads Image
      │
Creates Container
      │
Starts Container
```

---

# Docker CLI

The Docker CLI (Command Line Interface) is the tool users interact with.

Examples:

```bash
docker run
docker stop
docker ps
docker images
docker pull
docker push
docker build
```

The CLI communicates with the Docker Daemon using the Docker REST API.

---

# Docker REST API

The REST API acts as the communication layer between the Docker CLI and the Docker Daemon.

It allows:

- Docker CLI
- Docker Desktop
- CI/CD Pipelines
- IDEs
- Automation Tools

to communicate with Docker programmatically.

Example workflow:

```text
VS Code
    │
Docker CLI
    │
REST API
    │
Docker Daemon
```

---

# Container Runtime

Docker uses **containerd** as its container runtime.

Containerd is responsible for:

- Creating containers
- Starting containers
- Stopping containers
- Managing container lifecycle

Containerd further uses **runc** to actually launch the container.

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

# How Docker Works Internally

Suppose you run:

```bash
docker run nginx
```

The following steps occur:

1. Docker CLI receives the command.
2. CLI sends request to Docker Daemon.
3. Daemon checks if the image exists locally.
4. If not available, downloads from Docker Hub.
5. Creates writable container layer.
6. Starts the container process.
7. Returns Container ID.

---

# Linux Kernel Sharing

Unlike Virtual Machines, containers **share the host Linux Kernel**.

Example:

```text
Ubuntu Container
Fedora Container
AlmaLinux Container
Debian Container
        │
        ▼
 Shared Linux Kernel
        │
 Docker Engine
        │
 Hardware
```

Since the kernel is shared:

- Containers start in seconds.
- Containers consume less memory.
- Better CPU utilization.
- Higher density compared to VMs.

---

# Docker Editions

Earlier Docker had two editions:

- Community Edition (CE)
- Enterprise Edition (EE)

Today Docker primarily provides:

- Docker Engine
- Docker Desktop

---

# Docker Subscription Plans

Docker offers multiple subscription plans.

| Plan | Target Users |
|--------|--------------|
| Personal | Individual Developers |
| Pro | Professional Developers |
| Team | Small Teams |
| Business | Enterprises |

---

# Architecture Diagram

```text
                   Docker CLI
                        │
                        ▼
                 Docker REST API
                        │
                        ▼
                 Docker Daemon
     ┌──────────┬──────────┬──────────┐
     │          │          │          │
 Images    Containers   Networks   Volumes
                        │
                        ▼
                  containerd
                        │
                        ▼
                      runc
                        │
                        ▼
                  Linux Kernel
                        │
                        ▼
                     Hardware
```

---

# Why Docker Uses a Daemon

Instead of each command managing containers directly, Docker centralizes operations through the daemon.

Benefits:

- Better resource management
- Shared image cache
- Network management
- Volume management
- Easier automation

---

# Advantages of Docker Architecture

✅ Modular

✅ Lightweight

✅ Easy automation

✅ REST API support

✅ Scalable

✅ Platform independent

✅ Fast container startup

---

# Best Practices

- Always use Docker Engine from official sources.
- Keep Docker updated.
- Avoid running Docker as the root user unless necessary.
- Use Docker CLI for manual operations.
- Use the REST API for automation.
- Monitor Docker Daemon logs during troubleshooting.

---

# Quick Revision

```text
Docker CLI
      │
REST API
      │
Docker Daemon (dockerd)
      │
containerd
      │
runc
      │
Linux Kernel
      │
Containers
```

---

# Interview Questions

## 1. What are the main components of Docker Architecture?

- Docker CLI
- Docker Daemon
- Docker REST API
- containerd
- runc
- Linux Kernel

---

## 2. What is Docker Daemon?

A background service that manages Docker objects such as images, containers, networks, and volumes.

---

## 3. What is containerd?

A container runtime responsible for managing the lifecycle of containers.

---

## 4. What is runc?

A lightweight runtime that creates and starts containers according to the OCI specification.

---

## 5. How does Docker CLI communicate with Docker Daemon?

Using the Docker REST API.

---

## 6. Why are Docker containers lightweight?

Because they share the host operating system kernel instead of running a separate guest operating system.

---

# Summary

Docker follows a client-server architecture where the Docker CLI communicates with the Docker Daemon using the Docker REST API. The daemon relies on containerd and runc to create and manage containers that share the host Linux kernel. This architecture enables Docker to provide fast, lightweight, and portable application deployment across different environments.