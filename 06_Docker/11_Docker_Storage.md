# 💽 Docker Storage

Docker Storage determines how data is stored, managed, and persisted inside containers. Understanding Docker Storage is essential because containers are **ephemeral**—any data written inside a container's writable layer is lost when the container is removed unless persistent storage is configured.

---

# Table of Contents

- [What is Docker Storage?](#what-is-docker-storage)
- [Container Filesystem](#container-filesystem)
- [Read-Only and Writable Layers](#read-only-and-writable-layers)
- [Storage Drivers](#storage-drivers)
- [Copy-on-Write (CoW)](#copy-on-write-cow)
- [Docker Root Directory](#docker-root-directory)
- [Docker Storage Commands](#docker-storage-commands)
- [Practical Examples](#practical-examples)
- [Storage Workflow](#storage-workflow)
- [Common Mistakes](#common-mistakes)
- [Best Practices](#best-practices)
- [Quick Revision](#quick-revision)
- [Interview Questions](#interview-questions)

---

# What is Docker Storage?

Docker Storage is the mechanism Docker uses to manage:

- Images
- Containers
- Volumes
- Build Cache
- Networks Metadata

Docker stores these resources under its root directory.

Default location on Linux:

```text
/var/lib/docker/
```

---

# Container Filesystem

Every container consists of:

```text
Application Layer
        │
Writable Layer
────────────────────
Image Layer 3
────────────────────
Image Layer 2
────────────────────
Image Layer 1
────────────────────
Base Image
```

The image layers are **read-only**.

Only the top writable layer changes while the container is running.

---

# Read-Only and Writable Layers

## Read-Only Layers

- Created during image build
- Shared among multiple containers
- Cannot be modified

Examples

```text
Ubuntu Base Image

Python Packages

Application Dependencies
```

---

## Writable Layer

Created when a container starts.

Contains:

- Temporary Files
- Logs
- Runtime Changes
- Installed Packages (inside container)

If the container is removed,

❌ Writable layer is deleted.

---

# Storage Drivers

Storage drivers manage image layers efficiently.

Common drivers:

| Driver | Description |
|---------|-------------|
| overlay2 | Recommended Linux storage driver |
| aufs | Older Ubuntu driver |
| btrfs | Btrfs filesystem |
| zfs | ZFS filesystem |
| devicemapper | Legacy driver |

To check the current storage driver:

```bash
docker info
```

Example Output

```text
Storage Driver: overlay2
```

---

# Copy-on-Write (CoW)

Docker uses **Copy-on-Write (CoW)** technology.

Instead of copying the complete filesystem for every container,

Docker only copies files when they are modified.

Example

```text
Ubuntu Image
       │
       ├── Container A
       ├── Container B
       └── Container C
```

All containers share the same image layers.

If Container A modifies a file:

```text
Image Layer
        │
Container A
Writable Copy
```

Only the modified file is copied.

Benefits

- Faster startup
- Lower storage usage
- Better performance

---

# Docker Root Directory

Docker stores data in

```text
/var/lib/docker/
```

Typical structure

```text
/var/lib/docker/

├── containers/

├── image/

├── volumes/

├── overlay2/

├── network/

├── buildkit/
```

---

# Docker Storage Commands

| Command | Description |
|----------|-------------|
| `docker info` | Display storage driver |
| `docker system df` | Show Docker disk usage |
| `docker system prune` | Remove unused resources |
| `docker image prune` | Remove unused images |
| `docker volume ls` | List volumes |
| `docker volume inspect` | View volume location |

---

# Practical Examples

## View Storage Driver

```bash
docker info
```

Expected Output

```text
Storage Driver: overlay2
```

Use Case

Verify the storage driver being used on a production server.

---

## Check Docker Disk Usage

```bash
docker system df
```

Expected Output

```text
TYPE            TOTAL

Images          10

Containers      5

Volumes         4

Build Cache     2
```

Use Case

Identify which Docker resources consume disk space.

---

## Remove Unused Resources

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

Free disk space on development or CI/CD servers.

---

## Remove Unused Images

```bash
docker image prune
```

Use Case

Delete dangling images created during development.

---

## List Volumes

```bash
docker volume ls
```

Use Case

Verify persistent storage used by databases.

---

## Inspect Volume

```bash
docker volume inspect mysql-data
```

Expected Output

```json
[
 {
   "Name": "mysql-data",
   "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data"
 }
]
```

Use Case

Locate where Docker stores persistent data.

---

# Storage Workflow

```text
Dockerfile
      │
Build Image
      │
Read-Only Layers
      │
docker run
      │
Writable Layer
      │
Application Writes Data
      │
Volume (Optional)
      │
Persistent Storage
```

---

# Common Mistakes

❌ Storing databases inside the writable layer.

❌ Forgetting that container storage is temporary.

❌ Deleting volumes accidentally.

❌ Ignoring Docker disk usage.

❌ Using old storage drivers.

---

# Best Practices

- Use **overlay2** whenever possible.
- Store important data in Docker Volumes.
- Clean unused images regularly.
- Monitor Docker storage usage.
- Use named volumes for production applications.
- Avoid storing logs inside containers.

---

# Quick Revision

```text
Read-Only Layers
        │
Shared by Containers

Writable Layer
        │
Temporary Storage

overlay2
        │
Recommended Driver

docker info
        │
Storage Driver

docker system df
        │
Disk Usage

docker system prune
        │
Cleanup
```

---

# Interview Questions

## 1. What is Docker Storage?

Docker Storage is the mechanism used to store images, containers, volumes, and build cache.

---

## 2. What is the writable layer?

A temporary layer created when a container starts. It stores runtime changes and is deleted when the container is removed.

---

## 3. What is Copy-on-Write?

Copy-on-Write allows containers to share image layers while creating writable copies only for modified files, reducing storage usage.

---

## 4. Which storage driver is recommended on Linux?

```text
overlay2
```

---

## 5. Where does Docker store its data?

Default location:

```text
/var/lib/docker/
```

---

## 6. How do you check Docker disk usage?

```bash
docker system df
```

---

## 7. Which command displays the active storage driver?

```bash
docker info
```

---

# Summary

Docker Storage uses layered filesystems and Copy-on-Write technology to efficiently manage images and containers. Read-only image layers are shared across containers, while each container receives its own writable layer for runtime changes. Persistent data should always be stored in Docker Volumes rather than the container's writable layer. Understanding storage drivers such as **overlay2**, Docker's root directory, and storage management commands is essential for maintaining efficient, reliable, and scalable containerized applications.