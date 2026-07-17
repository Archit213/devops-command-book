# 🐳 Docker Introduction

Docker is an open-source containerization platform that packages an application along with all its dependencies, libraries, and runtime into a lightweight, portable unit called a **container**.

It solves the classic **"It works on my machine"** problem by ensuring that an application behaves the same across different environments.

---

# Table of Contents

- [Why Docker?](#why-docker)
- [Problems Before Docker](#problems-before-docker)
- [What is Docker?](#what-is-docker)
- [What is a Container?](#what-is-a-container)
- [How Docker Solves the Problem](#how-docker-solves-the-problem)
- [Container vs Virtual Machine](#container-vs-virtual-machine)
- [Benefits of Docker](#benefits-of-docker)
- [Docker Workflow](#docker-workflow)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# Why Docker?

Modern applications are made up of multiple services that work together.

For example:

- Web Server (Node.js)
- Database (MongoDB)
- Messaging Queue (Redis)
- Orchestration Tools (Ansible)

Each component depends on different:

- Operating Systems
- Libraries
- Dependencies
- Runtime Versions

Installing and configuring all of these manually on every machine is time-consuming and error-prone.

Docker eliminates this problem by packaging everything required to run an application inside a container.

---

# Problems Before Docker

Before Docker, developers manually installed dependencies on their local systems.

Example:

| Developer | OS | Node Version | MongoDB | Redis |
|-----------|----|--------------|----------|--------|
| Developer A | macOS | v18 | 4.4 | 6.2 |
| Developer B | Ubuntu | v16 | 5.0 | 7.0 |
| Developer C | Windows | v20 | Latest | Latest |

The same application might work on one system but fail on another because of:

- Different operating systems
- Different library versions
- Missing dependencies
- Configuration mismatches

This led to the common issue:

> **"It works on my machine."**

---

# What is Docker?

Docker is a containerization platform that packages:

- Application Code
- Libraries
- Dependencies
- Runtime
- Configuration

into a **Docker Image**, from which one or more **Containers** can be created.

Instead of configuring every server manually, you simply distribute the image and run the container.

---

# What is a Container?

A **Container** is a lightweight, isolated environment that contains:

- Application
- Dependencies
- Libraries
- Runtime
- Processes
- Network Interfaces
- Mount Points

Containers share the host operating system kernel while remaining isolated from one another.

Unlike Virtual Machines, containers **do not require a full guest operating system**.

---

# How Docker Solves the Problem

Traditional Deployment:

```text
Application
      ↓
Install Dependencies
      ↓
Configure Runtime
      ↓
Fix Version Issues
      ↓
Deploy
```

Docker Deployment:

```text
Docker Image
      ↓
docker run
      ↓
Container Running
```

One image can create multiple identical containers.

```text
Docker Image
      │
      ├── Container 1
      ├── Container 2
      └── Container 3
```

This guarantees consistent behavior across development, testing, and production environments.

---

# Container vs Virtual Machine

| Feature | Container | Virtual Machine |
|----------|-----------|-----------------|
| Boot Time | Seconds | Minutes |
| Size | MBs | GBs |
| Performance | Near Native | Higher Overhead |
| OS Included | No | Yes |
| Kernel | Shared Host Kernel | Own Guest OS |
| Resource Usage | Low | High |
| Isolation | Process Level | Hardware Level |

### Containers

```text
Application
Libraries
Dependencies
──────────────
Docker Engine
──────────────
Host OS
──────────────
Hardware
```

### Virtual Machines

```text
Application
Libraries
Dependencies
Guest OS
──────────────
Hypervisor
──────────────
Host OS
──────────────
Hardware
```

---

# Benefits of Docker

✅ Lightweight

✅ Fast startup

✅ Portable

✅ Consistent environments

✅ Better resource utilization

✅ Easy deployment

✅ Easy scaling

✅ Supports CI/CD workflows

---

# Docker Workflow

```text
Developer
     │
     ▼
Write Application
     │
     ▼
Create Dockerfile
     │
     ▼
Build Docker Image
     │
     ▼
Push Image to Registry
     │
     ▼
Pull Image Anywhere
     │
     ▼
Run Container
```

---

# Key Terminology

| Term | Description |
|------|-------------|
| Docker | Containerization Platform |
| Image | Read-only template used to create containers |
| Container | Running instance of an image |
| Docker Hub | Public image registry |
| Registry | Stores Docker images |
| Dockerfile | Blueprint used to build images |
| Docker Engine | Core runtime that runs containers |

---

# Where Docker is Used

Docker is commonly used for:

- Web Applications
- APIs
- Microservices
- Databases
- CI/CD Pipelines
- Development Environments
- Testing Environments
- Cloud Deployments

---

# Advantages over Traditional Deployment

Traditional Deployment

- Manual installation
- Version conflicts
- Environment mismatch
- Difficult scaling

Docker Deployment

- One command deployment
- Identical environments
- Easy scaling
- Faster releases
- Simplified maintenance

---

# Best Practices

- Use official Docker images whenever possible.
- Keep images small.
- Tag images with specific versions instead of `latest`.
- Run one main process per container.
- Store images in a registry.
- Avoid unnecessary software inside containers.

---

# Quick Revision

```text
Docker
│
├── Packages application + dependencies
├── Solves "Works on my machine"
├── Creates Containers from Images
├── Lightweight
├── Fast Startup
├── Portable
└── Shares Host OS Kernel
```

---

# Interview Questions

### 1. What problem does Docker solve?

Docker eliminates environment inconsistencies by packaging the application along with all required dependencies into a portable container.

---

### 2. What is a Docker Container?

A lightweight isolated environment that contains everything needed to run an application.

---

### 3. What is a Docker Image?

A read-only template used to create one or more Docker containers.

---

### 4. Difference between Container and Virtual Machine?

Containers share the host operating system kernel, whereas virtual machines include a complete guest operating system.

---

### 5. Why are containers lightweight?

Because they share the host operating system kernel instead of running a separate guest operating system.

---

# Summary

Docker is a containerization platform that packages applications with their dependencies into portable containers. It enables applications to run consistently across different environments while consuming fewer resources than traditional virtual machines, making it a foundational technology in modern DevOps and cloud-native development.