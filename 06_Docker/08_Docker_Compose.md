# 🐙 Docker Compose

Docker Compose is a tool used to define and manage **multi-container Docker applications** using a single YAML configuration file (`compose.yaml` or `docker-compose.yml`).

Instead of running multiple `docker run` commands manually, Docker Compose allows you to start, stop, build, and manage an entire application stack with a single command.

---

# Table of Contents

- [What is Docker Compose?](#what-is-docker-compose)
- [Why Docker Compose?](#why-docker-compose)
- [How Docker Compose Works](#how-docker-compose-works)
- [Compose File Structure](#compose-file-structure)
- [Docker Compose Commands](#docker-compose-commands)
- [Practical Examples](#practical-examples)
- [Environment Variables](#environment-variables)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is Docker Compose?

Docker Compose is an orchestration tool for running **multiple containers together**.

It uses a YAML file to define:

- Services
- Networks
- Volumes
- Environment Variables
- Port Mapping
- Dependencies

Instead of running:

```bash
docker run ...

docker run ...

docker run ...
```

you simply execute:

```bash
docker compose up
```

---

# Why Docker Compose?

Consider a web application consisting of:

- React Frontend
- Node.js Backend
- MySQL Database
- Redis Cache

Without Docker Compose, you would need to manually:

- Create networks
- Create volumes
- Start database
- Start backend
- Start frontend

Compose automates all of these tasks.

---

# How Docker Compose Works

```text
compose.yaml
       │
docker compose up
       │
───────────────
Frontend
Backend
Database
Redis
───────────────
Running Together
```

---

# Compose File Structure

A Compose file is written in **YAML**.

Example:

```yaml
services:

  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql:8
```

Main sections:

- services
- volumes
- networks
- environment
- ports
- depends_on

---

# Docker Compose Commands

| Command | Description |
|----------|-------------|
| `docker compose up` | Create and start all services |
| `docker compose up -d` | Run services in background |
| `docker compose down` | Stop and remove services |
| `docker compose ps` | List running services |
| `docker compose logs` | View logs |
| `docker compose stop` | Stop services |
| `docker compose start` | Start stopped services |
| `docker compose restart` | Restart services |
| `docker compose build` | Build images |
| `docker compose pull` | Pull latest images |
| `docker compose config` | Validate compose file |

---

# Practical Examples

## Start Services

Purpose

Start every service defined inside the Compose file.

Syntax

```bash
docker compose up
```

Example

```bash
docker compose up
```

Expected Output

```text
Creating network "app_default"

Creating mysql

Creating backend

Creating frontend

Attaching to...
```

Use Case

Deploy an entire application stack during development.

---

## Start in Detached Mode

```bash
docker compose up -d
```

Expected Output

```text
Creating...

Done
```

Use Case

Run applications in the background without occupying the terminal.

---

## Stop Everything

```bash
docker compose down
```

Expected Output

```text
Stopping frontend

Stopping backend

Stopping mysql

Removing containers

Removing network
```

Use Case

Cleanly shut down the complete application stack.

---

## View Running Services

```bash
docker compose ps
```

Expected Output

```text
NAME

STATE

PORTS
```

Use Case

Verify which services are running.

---

## View Logs

```bash
docker compose logs
```

Example

```bash
docker compose logs backend
```

Use Case

Troubleshoot application startup issues.

---

## Stop Services

```bash
docker compose stop
```

Stops containers without removing them.

---

## Restart Services

```bash
docker compose restart
```

Useful after configuration changes.

---

## Build Images

```bash
docker compose build
```

Use Case

Rebuild application images after source code changes.

---

## Pull Latest Images

```bash
docker compose pull
```

Downloads updated images before deployment.

---

## Validate Compose File

```bash
docker compose config
```

Expected Output

```text
services:

frontend:

backend:

database:
```

Use Case

Verify YAML syntax before deployment.

---

# Environment Variables

Compose supports environment variables.

Example

```yaml
environment:
  MYSQL_ROOT_PASSWORD=password
  MYSQL_DATABASE=appdb
```

You can also use a `.env` file.

Example

```text
DB_HOST=mysql

DB_PORT=3306

APP_ENV=production
```

---

# Networking in Compose

By default, Docker Compose creates its own bridge network.

Example

```text
Frontend
      │
Backend
      │
Database
```

Services communicate using their **service names**.

Example

```text
mysql

backend

frontend
```

No manual IP configuration is required.

---

# Common Mistakes

❌ Incorrect YAML indentation

❌ Forgetting `-d` for background execution

❌ Hardcoding container IP addresses

❌ Not rebuilding images after source code changes

❌ Using `latest` images in production

---

# Best Practices

- Keep one service per container.
- Use named volumes for persistent data.
- Store secrets outside the Compose file.
- Pin image versions.
- Use `.env` files for configuration.
- Validate Compose files before deployment.

---

# Quick Revision

```text
docker compose up
        │
Start Services

docker compose up -d
        │
Background Mode

docker compose down
        │
Stop + Remove

docker compose ps
        │
Running Services

docker compose logs
        │
View Logs

docker compose restart
        │
Restart Services

docker compose build
        │
Build Images

docker compose pull
        │
Download Images

docker compose config
        │
Validate YAML
```

---

# Interview Questions

## 1. What is Docker Compose?

Docker Compose is a tool used to define and manage multi-container Docker applications using a YAML configuration file.

---

## 2. Why use Docker Compose?

It allows multiple related containers to be started, stopped, and managed together with a single command.

---

## 3. What file does Docker Compose use?

- `compose.yaml` *(recommended)*
- `docker-compose.yml` *(legacy but still supported)*

---

## 4. Difference between `docker run` and `docker compose up`?

| docker run | docker compose up |
|------------|-------------------|
| Starts one container | Starts multiple services |
| Manual configuration | YAML-based configuration |
| Best for simple containers | Best for complete applications |

---

## 5. What happens when `docker compose down` is executed?

It stops and removes:

- Containers
- Networks

By default, named volumes are preserved unless `-v` is specified.

---

## 6. Why are service names used instead of IP addresses?

Docker Compose automatically creates an internal DNS server that resolves service names to container IP addresses.

---

# Summary

Docker Compose simplifies the deployment of multi-container applications by allowing developers to define services, networks, volumes, and environment variables in a single YAML file. It is widely used in local development, testing, and CI/CD workflows because it provides a consistent, repeatable, and easily maintainable deployment process.