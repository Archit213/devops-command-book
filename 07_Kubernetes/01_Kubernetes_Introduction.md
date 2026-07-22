# ☸️ Kubernetes (K8s) Introduction

## What is Kubernetes?

Kubernetes (also known as **K8s**) is an open-source **container orchestration platform** originally developed by **Google**.

It is used to deploy, manage, scale, and automate containerized applications.

---

# Container Orchestration

Container orchestration means managing multiple containers automatically.

Instead of manually starting, stopping, scaling, and monitoring containers, Kubernetes performs these tasks automatically.

---

# Traditional Environment

```text
Application
│
├── Web Server (NodeJS)
├── Database (MongoDB)
├── Messaging (Redis)
├── Libraries
├── Dependencies
└── Operating System
        │
Hardware Infrastructure
```

---

# Problems in Traditional Deployments

According to the notes:

✅ OS Compatibility Issues

Different operating systems may behave differently.

Example:

```
Works on Ubuntu

↓

Fails on CentOS
```

---

✅ Dependency Issues

Different library versions cause applications to fail.

Example

```
NodeJS v18

↓

Application built

↓

Production server has NodeJS v16

↓

Application crashes
```

---

## Docker Solution

Docker packages

- Application
- Libraries
- Dependencies

inside a container.

Developers only need Docker installed.

```text
Developer

↓

Build Docker Image

↓

Docker Container

↓

Runs on Any Docker Host
```

---

# Why Kubernetes?

Docker manages individual containers.

When an application grows:

- More users
- More traffic
- Multiple containers
- Multiple hosts

Managing containers manually becomes difficult.

Kubernetes solves this problem.

---

# Container Orchestration

```text
Docker Host 1
┌─────────────┐
│ Web         │
└─────────────┘

Docker Host 2
┌─────────────┐
│ Web         │
└─────────────┘

Docker Host 3
┌─────────────┐
│ Web         │
└─────────────┘

           ▲

 Kubernetes

           │

Automatically manages all containers
```

---

# Features Mentioned

- Deployment
- Scaling
- Scale Up
- Scale Down
- Container Management

---

# Quick Revision

```text
Traditional Deployment

↓

Compatibility Issues

↓

Docker

↓

Containers

↓

Multiple Containers

↓

Kubernetes

↓

Container Orchestration
```

---

# Summary

- Kubernetes is also known as K8s.
- It was originally developed by Google.
- Kubernetes is a container orchestration platform.
- Docker packages applications and dependencies into containers.
- Kubernetes automates deployment, scaling, and management of containers.