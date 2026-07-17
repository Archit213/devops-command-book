# ⚙️ Docker Installation

This guide explains how to install Docker Engine on a Linux system, verify the installation, and understand the basic setup required before working with Docker containers.

---

# Table of Contents

- [Prerequisites](#prerequisites)
- [Installation Overview](#installation-overview)
- [Check Operating System](#check-operating-system)
- [Check System Architecture](#check-system-architecture)
- [Remove Older Docker Versions](#remove-older-docker-versions)
- [Install Docker Engine](#install-docker-engine)
- [Verify Installation](#verify-installation)
- [Start Docker Service](#start-docker-service)
- [Run Your First Container](#run-your-first-container)
- [Docker Installation Workflow](#docker-installation-workflow)
- [Common Errors](#common-errors)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# Prerequisites

Before installing Docker:

- Linux Operating System (Ubuntu, Debian, CentOS, RHEL, etc.)
- Internet Connection
- sudo privileges
- 64-bit Operating System

---

# Installation Overview

Docker Engine is installed on the host operating system.

Typical installation flow:

```text
Check OS
      │
Check Architecture
      │
Remove Old Docker Packages
      │
Add Docker Repository
      │
Install Docker Engine
      │
Start Docker Service
      │
Verify Installation
      │
Run First Container
```

---

# Check Operating System

Before installation, verify your Linux distribution.

## Ubuntu

```bash
cat /etc/os-release
```

Example Output

```text
NAME="Ubuntu"
VERSION="22.04.4 LTS"
ID=ubuntu
```

---

## CentOS / RHEL

```bash
cat /etc/redhat-release
```

Example Output

```text
CentOS Stream release 9
```

---

# Check System Architecture

Docker Engine supports only 64-bit architectures.

```bash
dpkg --print-architecture
```

Example Output

```text
amd64
```

Other possible outputs:

```text
arm64

armhf

ppc64le
```

---

# Remove Older Docker Versions

Before installing Docker Engine, uninstall any old Docker packages.

Ubuntu:

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

CentOS/RHEL:

```bash
sudo yum remove docker*
```

Removing old packages prevents dependency conflicts.

---

# Install Docker Engine

The recommended installation method is from Docker's official repository.

Ubuntu Example

```bash
sudo apt update
```

```bash
sudo apt install docker-ce docker-ce-cli containerd.io
```

CentOS Example

```bash
sudo yum install docker-ce docker-ce-cli containerd.io
```

---

# Verify Installation

Check Docker version.

```bash
docker --version
```

Example Output

```text
Docker version 28.3.2
```

---

Check detailed information.

```bash
docker info
```

Example Output

```text
Containers: 0

Images: 0

Server Version: 28.3.2
```

---

# Start Docker Service

Start Docker

```bash
sudo systemctl start docker
```

Check Status

```bash
sudo systemctl status docker
```

Enable Docker on Boot

```bash
sudo systemctl enable docker
```

Expected Output

```text
Created symlink ...

docker.service enabled
```

---

# Run Your First Container

Run nginx

```bash
docker run nginx
```

Expected Output

```text
Unable to find image 'nginx:latest' locally

latest: Pulling from library/nginx

Status: Downloaded newer image

...
```

---

Run Ubuntu

```bash
docker run ubuntu
```

Docker downloads the Ubuntu image, starts the container, and exits immediately because no foreground process is running.

---

Run Ubuntu for 5 seconds

```bash
docker run ubuntu sleep 5
```

The container automatically exits after five seconds.

---

# Verify Running Containers

```bash
docker ps
```

Example Output

```text
CONTAINER ID

IMAGE

STATUS

PORTS

NAMES
```

Show all containers

```bash
docker ps -a
```

---

# Docker Installation Workflow

```text
Linux Host
      │
Install Docker Engine
      │
Docker Daemon Starts
      │
Docker CLI Installed
      │
Run docker run nginx
      │
Download Image
      │
Create Container
      │
Application Running
```

---

# Common Errors

## docker: command not found

Cause:

Docker is not installed or PATH is incorrect.

Solution:

Install Docker Engine.

---

## Cannot connect to Docker daemon

Cause:

Docker service is stopped.

Solution:

```bash
sudo systemctl start docker
```

---

## Permission denied

Cause:

Current user is not part of docker group.

Solution

```bash
sudo usermod -aG docker $USER
```

Logout and login again.

---

## Unsupported Architecture

Cause

Running Docker on unsupported CPU architecture.

Check using

```bash
dpkg --print-architecture
```

---

# Best Practices

- Install Docker from the official repository.
- Keep Docker updated.
- Remove unused Docker packages before reinstalling.
- Verify Docker after installation.
- Enable Docker to start automatically during boot.
- Avoid running containers as the root user whenever possible.

---

# Quick Revision

```text
Check OS

cat /etc/os-release

--------------------------------

Check Architecture

dpkg --print-architecture

--------------------------------

Install Docker

apt install docker-ce

--------------------------------

Verify

docker --version

docker info

--------------------------------

Start Docker

systemctl start docker

--------------------------------

Run First Container

docker run nginx
```

---

# Interview Questions

## 1. Why should Docker be installed from the official repository?

The official repository provides the latest stable Docker Engine, security updates, and compatibility fixes.

---

## 2. How do you check whether Docker is installed?

```bash
docker --version
```

---

## 3. How do you verify Docker is running?

```bash
systemctl status docker
```

---

## 4. Why does `docker run ubuntu` exit immediately?

Because Ubuntu has no foreground process running after the container starts.

---

## 5. How do you automatically start Docker after reboot?

```bash
systemctl enable docker
```

---

# Summary

Docker Engine installation involves verifying the operating system and architecture, removing conflicting Docker packages, installing Docker from the official repository, starting the Docker service, and validating the installation by running a test container. Following these steps ensures a stable Docker environment ready for development and production workloads.