# 🌐 Docker Networking

Docker Networking enables communication between containers, the host machine, and external networks. Every container is attached to a Docker network, allowing applications to communicate securely while remaining isolated from one another.

---

# Table of Contents

- [What is Docker Networking?](#what-is-docker-networking)
- [Why Docker Networking?](#why-docker-networking)
- [Types of Docker Networks](#types-of-docker-networks)
- [Bridge Network](#bridge-network)
- [Host Network](#host-network)
- [None Network](#none-network)
- [Overlay Network](#overlay-network)
- [Macvlan Network](#macvlan-network)
- [Docker Networking Commands](#docker-networking-commands)
- [Port Mapping](#port-mapping)
- [Container Communication](#container-communication)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is Docker Networking?

Docker Networking allows containers to communicate with:

- Other containers
- The host machine
- External clients
- Internet services

Each container receives its own:

- IP Address
- Network Interface
- DNS Resolution
- Routing Table

---

# Why Docker Networking?

Without networking:

- Containers cannot communicate.
- Applications like web servers cannot reach databases.
- External users cannot access services.

Example:

```text
Browser
    │
    ▼
Nginx Container
    │
    ▼
Backend API Container
    │
    ▼
MySQL Container
```

---

# Types of Docker Networks

Docker provides several network drivers.

| Network | Description |
|----------|-------------|
| Bridge | Default network for standalone containers |
| Host | Shares host network stack |
| None | No networking |
| Overlay | Multi-host container communication |
| Macvlan | Assigns MAC address to container |

---

# Bridge Network

The default Docker network.

Features:

- Private internal network
- Containers communicate using IP or container name
- Isolated from the host

Example

```bash
docker network ls
```

Output

```text
NETWORK ID

NAME

bridge

host

none
```

---

# Host Network

The container shares the host's network stack.

Benefits

- Better performance
- No NAT
- No port mapping required

Example

```bash
docker run --network host nginx
```

Use Case

High-performance applications requiring minimal network overhead.

---

# None Network

The container has no network connectivity.

Example

```bash
docker run --network none ubuntu
```

Use Case

Security-sensitive workloads that should not access any network.

---

# Overlay Network

Used in Docker Swarm.

Allows containers running on different hosts to communicate securely.

Example

```text
Server A
│
Container A
      │
Overlay Network
      │
Container B
│
Server B
```

---

# Macvlan Network

Assigns a real MAC address to each container.

Containers appear as physical devices on the LAN.

Commonly used for:

- Legacy applications
- Monitoring appliances
- Network appliances

---

# Docker Networking Commands

| Command | Description |
|----------|-------------|
| `docker network ls` | List networks |
| `docker network inspect NETWORK` | View network details |
| `docker network create NETWORK` | Create network |
| `docker network rm NETWORK` | Remove network |
| `docker network connect NETWORK CONTAINER` | Connect container |
| `docker network disconnect NETWORK CONTAINER` | Disconnect container |
| `docker network prune` | Remove unused networks |

---

# Port Mapping

Containers are isolated.

To expose an application outside the container:

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE
```

Example

```bash
docker run -d -p 8080:80 nginx
```

Meaning

```text
Host Port      8080
        │
        ▼
Container Port 80
```

Access:

```
http://localhost:8080
```

---

# Container Communication

Containers on the same bridge network can communicate using their names.

Example

```text
frontend
     │
     ▼
backend
     │
     ▼
database
```

No IP address needs to be remembered.

Docker's embedded DNS resolves container names automatically.

---

# Practical Examples

## List Networks

```bash
docker network ls
```

Use Case

View all available Docker networks.

---

## Create Network

```bash
docker network create my-network
```

Output

```text
8a0ef29d18d...
```

Use Case

Create an isolated network for microservices.

---

## Inspect Network

```bash
docker network inspect my-network
```

Use Case

View connected containers, subnet, gateway, and driver information.

---

## Run Container on Custom Network

```bash
docker run -d --network my-network nginx
```

Use Case

Deploy an application inside a dedicated network.

---

## Connect Existing Container

```bash
docker network connect my-network backend
```

Use Case

Connect a running container to another network without recreating it.

---

## Disconnect Container

```bash
docker network disconnect my-network backend
```

Use Case

Remove unnecessary network access.

---

## Remove Network

```bash
docker network rm my-network
```

Use Case

Delete unused custom networks.

---

## Remove Unused Networks

```bash
docker network prune
```

Use Case

Clean up orphaned Docker networks.

---

# Common Mistakes

❌ Forgetting to publish ports using `-p`

❌ Placing unrelated applications on the same network

❌ Using Host networking unnecessarily

❌ Hardcoding container IP addresses

❌ Creating too many unused networks

---

# Best Practices

- Use custom bridge networks instead of the default bridge.
- Communicate using container names instead of IP addresses.
- Publish only required ports.
- Remove unused networks regularly.
- Separate frontend, backend, and database networks where appropriate.
- Use Overlay networks for Docker Swarm deployments.

---

# Quick Revision

```text
docker network ls
        │
List Networks

docker network create
        │
Create Network

docker network inspect
        │
View Details

docker network connect
        │
Connect Container

docker network disconnect
        │
Disconnect Container

docker network rm
        │
Delete Network

docker network prune
        │
Cleanup Networks

docker run -p
        │
Port Mapping
```

---

# Interview Questions

### 1. What is the default Docker network?

**Bridge Network**

---

### 2. What is the difference between Bridge and Host networking?

**Bridge**
- Isolated
- Uses NAT
- Requires port mapping

**Host**
- Shares host network
- No NAT
- Better performance

---

### 3. What is the purpose of `docker network create`?

It creates a custom network so containers can communicate in an isolated environment.

---

### 4. Why is port mapping required?

Containers are isolated from the host. Port mapping exposes a container's service to external users.

---

### 5. How do containers communicate on the same network?

Using Docker's embedded DNS, which resolves container names to their IP addresses.

---

### 6. What is an Overlay Network?

A network driver that enables secure communication between containers running on different Docker hosts, typically used with Docker Swarm.

---

# Summary

Docker Networking provides secure and isolated communication between containers, the host, and external clients. By understanding network drivers, port mapping, DNS-based service discovery, and custom bridge networks, you can design scalable and maintainable containerized applications.