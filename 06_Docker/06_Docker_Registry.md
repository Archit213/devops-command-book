# 🌐 Docker Registry

A **Docker Registry** is a storage and distribution system for Docker Images. It allows developers and organizations to store, manage, version, and share container images across different environments.

Docker Hub is the default public registry, but organizations often use private registries for security and internal deployments.

---

# Table of Contents

- [What is a Docker Registry?](#what-is-a-docker-registry)
- [How Docker Registry Works](#how-docker-registry-works)
- [Public vs Private Registry](#public-vs-private-registry)
- [Docker Hub](#docker-hub)
- [Image Naming Convention](#image-naming-convention)
- [Docker Registry Commands](#docker-registry-commands)
- [Practical Examples](#practical-examples)
- [Registry Workflow](#registry-workflow)
- [Best Practices](#best-practices)
- [Common Mistakes](#common-mistakes)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is a Docker Registry?

A Docker Registry is a centralized repository that stores Docker Images.

Instead of transferring images manually between servers, images are pushed to a registry and later pulled by any machine that has permission to access it.

```text
Developer
     │
Build Image
     │
Push Image
     │
Docker Registry
     │
Pull Image
     │
Production Server
```

---

# Docker Hub

Docker Hub is Docker's official cloud-based registry.

It provides:

- Public repositories
- Private repositories
- Official Images
- Verified Publisher Images
- Automated Builds
- Image Versioning

Official Images include:

- nginx
- ubuntu
- alpine
- mysql
- redis
- postgres
- node
- python

---

# Public vs Private Registry

| Public Registry | Private Registry |
|----------------|-----------------|
| Accessible by everyone | Restricted access |
| Ideal for open-source projects | Used for enterprise applications |
| Docker Hub Public | AWS ECR, Azure ACR, GCR, Harbor, JFrog |

---

# Popular Docker Registries

| Registry | Provider |
|----------|----------|
| Docker Hub | Docker |
| Amazon ECR | AWS |
| Azure Container Registry (ACR) | Microsoft Azure |
| Google Artifact Registry | Google Cloud |
| Harbor | Open Source |
| JFrog Artifactory | JFrog |

---

# Image Naming Convention

Docker images follow this format:

```text
registry/repository/image:tag
```

Examples:

```text
nginx:latest

library/ubuntu:24.04

username/myapp:v1

mycompany/backend:v2

acr.azurecr.io/backend:v1
```

If no registry is specified:

Docker automatically uses

```text
docker.io
```

---

# Docker Registry Commands

| Command | Description |
|----------|-------------|
| `docker login` | Authenticate to a registry |
| `docker logout` | Logout from registry |
| `docker pull IMAGE` | Download image |
| `docker push IMAGE` | Upload image |
| `docker search IMAGE` | Search Docker Hub |
| `docker tag SOURCE TARGET` | Tag image before pushing |

---

# Registry Workflow

```text
Create Dockerfile
        │
docker build
        │
Docker Image
        │
docker tag
        │
docker login
        │
docker push
        │
Docker Registry
        │
docker pull
        │
Run Container
```

---

# Practical Examples

## Login to Docker Hub

Purpose

Authenticate with Docker Hub.

Syntax

```bash
docker login
```

Example

```bash
docker login
```

Expected Output

```text
Username: johndoe

Password:

Login Succeeded
```

Use Case

Authenticate before pushing private images.

---

## Logout

Syntax

```bash
docker logout
```

Expected Output

```text
Removing login credentials

Logout Succeeded
```

---

## Search Images

Purpose

Search Docker Hub.

Syntax

```bash
docker search nginx
```

Expected Output

```text
NAME

DESCRIPTION

STARS

OFFICIAL
```

Use Case

Find official images before downloading.

---

## Download Image

```bash
docker pull nginx
```

Expected Output

```text
Using default tag: latest

Pulling from library/nginx

Digest: sha256:...
```

---

## Tag an Image

Purpose

Rename an image before pushing.

Syntax

```bash
docker tag nginx username/nginx:v1
```

Expected Output

```text
$
```

Use Case

Prepare image for uploading to Docker Hub.

---

## Push Image

Purpose

Upload image to registry.

Syntax

```bash
docker push username/nginx:v1
```

Expected Output

```text
The push refers to repository

Layer already exists

latest: digest: sha256:...
```

Use Case

Deploy custom-built applications to a registry for use by development, staging, or production environments.

---

## Pull Image from Registry

```bash
docker pull username/nginx:v1
```

Use Case

Download image to another server before deployment.

---

# Registry Authentication

Before pushing an image:

```text
Build Image
      │
docker login
      │
Authentication
      │
docker push
```

Without authentication:

```text
denied: requested access to the resource is denied
```

---

# Versioning Images

Instead of:

```text
latest
```

Use:

```text
backend:v1.0.0

backend:v1.1.0

backend:v2.0.0
```

Benefits:

- Easy Rollback
- Predictable Deployments
- CI/CD Friendly

---

# Common Mistakes

❌ Forgetting to tag the image before pushing.

❌ Using the `latest` tag in production.

❌ Pushing large, unoptimized images.

❌ Not logging in before pushing.

❌ Accidentally making sensitive repositories public.

---

# Best Practices

- Use private registries for production applications.
- Tag images with semantic versions.
- Remove unused image tags.
- Keep repositories organized.
- Scan images for vulnerabilities.
- Store only production-ready images.
- Use CI/CD pipelines to automate image builds and pushes.

---

# Quick Revision

```text
docker login      → Login

docker logout     → Logout

docker search     → Search Images

docker pull       → Download Image

docker tag        → Rename Image

docker push       → Upload Image
```

---

# Interview Questions

## 1. What is a Docker Registry?

A Docker Registry is a centralized storage system used to store and distribute Docker Images.

---

## 2. What is Docker Hub?

Docker Hub is Docker's official cloud-based image registry that hosts both public and private repositories.

---

## 3. Why is `docker tag` required before `docker push`?

The image must include the correct repository name and tag so Docker knows where to upload it.

---

## 4. Difference between `docker pull` and `docker push`?

- `docker pull` downloads an image from a registry.
- `docker push` uploads an image to a registry.

---

## 5. Why should production images use version tags instead of `latest`?

Version tags provide predictable deployments, easier rollbacks, and better traceability in CI/CD pipelines.

---

## 6. Name some popular Docker Registries.

- Docker Hub
- Amazon Elastic Container Registry (ECR)
- Azure Container Registry (ACR)
- Google Artifact Registry
- Harbor
- JFrog Artifactory

---

# Summary

A Docker Registry stores and distributes Docker Images, enabling teams to share containerized applications efficiently. Docker Hub is the default public registry, while organizations commonly use private registries such as Azure Container Registry (ACR), Amazon ECR, or Harbor for secure deployments. Understanding image tagging, authentication, and push/pull workflows is fundamental for modern DevOps and CI/CD practices.