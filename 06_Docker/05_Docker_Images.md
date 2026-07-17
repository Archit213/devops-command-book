# 🖼️ Docker Images

A **Docker Image** is a lightweight, read-only template that contains everything required to run an application, including the application code, runtime, libraries, dependencies, and configuration files.

Containers are created from Docker Images.

---

# Table of Contents

- [What is a Docker Image?](#what-is-a-docker-image)
- [Image Architecture](#image-architecture)
- [Image Layers](#image-layers)
- [Image Tags](#image-tags)
- [Docker Image Commands](#docker-image-commands)
- [Image Lifecycle](#image-lifecycle)
- [Practical Examples](#practical-examples)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is a Docker Image?

A Docker Image is a **read-only blueprint** used to create one or more Docker Containers.

It contains:

- Application Code
- Runtime
- Libraries
- Dependencies
- Environment Variables
- Default Commands
- Metadata

An image itself does **not** run.

A running instance of an image is called a **Container**.

---

# Image Architecture

```text
Docker Image
      │
      ├── Container 1
      ├── Container 2
      ├── Container 3
      └── Container 4
```

One image can create thousands of containers.

---

# Image Layers

Docker Images are built in **layers**.

Each instruction in a Dockerfile creates a new layer.

Example:

```text
Application Files
────────────────────
Python Packages
────────────────────
Operating System Packages
────────────────────
Ubuntu Base Image
```

### Benefits of Layers

- Faster Builds
- Layer Caching
- Smaller Downloads
- Efficient Storage
- Reusable Components

---

# Image Tags

Images are identified using:

```text
repository:tag
```

Example

```text
nginx:latest

ubuntu:24.04

python:3.12

node:20
```

If no tag is specified, Docker automatically uses:

```text
latest
```

Example

```bash
docker pull nginx
```

is equivalent to

```bash
docker pull nginx:latest
```

---

# Docker Image Commands

| Command | Description |
|----------|-------------|
| `docker images` | List downloaded images |
| `docker image ls` | List images (new syntax) |
| `docker pull IMAGE` | Download image |
| `docker rmi IMAGE` | Remove image |
| `docker image rm IMAGE` | Remove image (new syntax) |
| `docker inspect IMAGE` | View image details |
| `docker history IMAGE` | Display image layers |
| `docker tag IMAGE NEW_IMAGE` | Create image tag |
| `docker save IMAGE` | Save image as tar file |
| `docker load` | Load saved image |
| `docker image prune` | Remove unused images |
| `docker image prune -a` | Remove all unused images |

---

# Image Lifecycle

```text
Dockerfile
      │
docker build
      │
Docker Image
      │
docker push
      │
Docker Registry
      │
docker pull
      │
Docker Image
      │
docker run
      │
Container
```

---

# Practical Examples

## 1. List Images

Purpose

Display all downloaded Docker images.

Syntax

```bash
docker images
```

Example

```bash
docker images
```

Expected Output

```text
REPOSITORY    TAG       IMAGE ID       CREATED

nginx         latest    6f715d38      3 weeks ago

ubuntu        24.04     7ff0d2d2      2 months ago
```

Use Case

Check whether an image already exists before downloading.

---

## 2. Download an Image

Purpose

Download an image from Docker Hub.

Syntax

```bash
docker pull IMAGE
```

Example

```bash
docker pull nginx
```

Expected Output

```text
Using default tag: latest

latest: Pulling from library/nginx

Digest: sha256:...
```

Use Case

Download required images before deployment.

---

## 3. Remove Image

Syntax

```bash
docker rmi nginx
```

Expected Output

```text
Untagged: nginx:latest

Deleted: sha256:...
```

Use Case

Free up disk space by removing unused images.

---

## 4. Inspect Image

Purpose

View detailed image information.

Syntax

```bash
docker inspect nginx
```

Expected Output

```json
[
 {
   "Id":"sha256:..."
 }
]
```

Use Case

Check image metadata and configuration.

---

## 5. View Image Layers

Syntax

```bash
docker history nginx
```

Expected Output

```text
IMAGE

CREATED

SIZE

COMMENT
```

Use Case

Understand image composition and optimize Dockerfiles.

---

## 6. Tag an Image

Purpose

Create another name for an image.

Syntax

```bash
docker tag SOURCE_IMAGE TARGET_IMAGE
```

Example

```bash
docker tag nginx myrepo/nginx:v1
```

Use Case

Tag images before pushing to a private registry.

---

## 7. Save an Image

Purpose

Export image as a tar archive.

Syntax

```bash
docker save nginx -o nginx.tar
```

Expected Output

```text
$
```

Use Case

Transfer Docker images without internet access.

---

## 8. Load an Image

Purpose

Import a previously exported image.

Syntax

```bash
docker load -i nginx.tar
```

Expected Output

```text
Loaded image: nginx:latest
```

Use Case

Restore Docker images on another machine.

---

## 9. Remove Unused Images

```bash
docker image prune
```

Use Case

Clean dangling images.

---

## 10. Remove All Unused Images

```bash
docker image prune -a
```

Use Case

Recover disk space on development servers.

---

# Image vs Container

| Docker Image | Docker Container |
|---------------|------------------|
| Read Only | Read Write |
| Template | Running Instance |
| Cannot Execute | Executes Application |
| Shared | Independent |
| Created using Dockerfile | Created using docker run |

---

# Common Mistakes

❌ Assuming an image is a running application.

❌ Using the `latest` tag in production.

❌ Downloading duplicate image versions.

❌ Removing images still being used by containers.

❌ Ignoring image size.

---

# Best Practices

- Use official images whenever possible.
- Pin specific image versions instead of `latest`.
- Remove unused images regularly.
- Keep images lightweight.
- Minimize the number of image layers.
- Tag images using semantic versioning.

Example:

```text
myapp:v1.0.0

myapp:v1.1.0

myapp:v2.0.0
```

---

# Quick Revision

```text
docker images           → List Images

docker pull             → Download Image

docker rmi              → Delete Image

docker inspect          → Image Details

docker history          → Image Layers

docker tag              → Create Tag

docker save             → Export Image

docker load             → Import Image

docker image prune      → Cleanup Images
```

---

# Interview Questions

## 1. What is a Docker Image?

A read-only template containing an application, dependencies, runtime, and configuration required to create Docker Containers.

---

## 2. Can multiple containers be created from one image?

Yes. A single Docker Image can be used to create any number of containers.

---

## 3. What are Docker Image layers?

Images are composed of multiple read-only layers created by each instruction in a Dockerfile. Layers improve storage efficiency and build performance.

---

## 4. What is the purpose of image tags?

Tags identify different versions of an image, such as `nginx:1.27` or `python:3.12`.

---

## 5. Difference between `docker pull` and `docker run`?

- `docker pull` only downloads the image.
- `docker run` creates and starts a container from the image.

---

## 6. Why should `latest` not be used in production?

Because the `latest` tag can change over time, making deployments unpredictable. Using fixed version tags ensures consistent and repeatable deployments.

---

# Summary

Docker Images are immutable, read-only templates used to create containers. They are built using layered filesystems, identified by repositories and tags, and stored in registries like Docker Hub. Understanding image management commands and best practices is essential for building efficient, secure, and reproducible containerized applications.