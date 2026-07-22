# 🏗️ Kubernetes Architecture

## Introduction

Kubernetes is a **Container Orchestration Technology** used to automate the deployment, management, scaling, and monitoring of containers running across multiple machines.

Some popular container orchestration technologies are:

- Kubernetes
- Docker Swarm
- Apache Mesos

Among these, Kubernetes is the most widely adopted orchestration platform.

---

# Why Container Orchestration?

As applications grow, manually managing containers becomes difficult.

Instead of managing containers individually, Kubernetes orchestrates them across multiple machines.

```text
                   Kubernetes
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     Node 1         Node 2         Node 3
   ┌─────────┐    ┌─────────┐    ┌─────────┐
   │  Web    │    │  Web    │    │  Web    │
   │Backend  │    │Backend  │    │Backend  │
   └─────────┘    └─────────┘    └─────────┘
```

Kubernetes automatically distributes and manages containers across all available nodes.

---

# Node

A **Node** is a physical or virtual machine where Kubernetes is installed.

It is the machine where application containers actually run.

```text
+----------------------+
|        Node          |
|                      |
|   ┌─────────────┐    |
|   │ Containers  │    |
|   └─────────────┘    |
+----------------------+
```

### Characteristics

- Physical machine or Virtual Machine
- Worker machine
- Runs application containers
- Managed by Kubernetes

---

# Cluster

A **Cluster** is a collection of multiple Nodes grouped together.

```text
                 Cluster

      ┌────────┐
      │ Node 1 │
      └────────┘

      ┌────────┐
      │ Node 2 │
      └────────┘

      ┌────────┐
      │ Node 3 │
      └────────┘
```

### Benefits of a Cluster

- High Availability
- Better Performance
- Fault Tolerance
- Easy Scaling
- Load Distribution

---

# Master Node

The **Master Node** manages all Worker Nodes inside the cluster.

It is responsible for:

- Managing the cluster
- Orchestrating containers
- Scheduling workloads
- Monitoring node health
- Scaling applications
- Recovering failed workloads

```text
                 Master Node
                      │
      ┌───────────────┼───────────────┐
      │               │               │
   Worker 1       Worker 2       Worker 3
```

---

# High Availability

Using multiple nodes improves application availability.

```text
Application

↓

Node 1

↓

Node Failure

↓

Application moved to another Node

↓

Application remains available
```

This prevents a single machine failure from causing application downtime.

---

# Scaling

Kubernetes supports:

### Scale Up

Increase the number of application instances.

```text
Web

↓

Web
Web
Web
```

---

### Scale Down

Reduce the number of running instances.

```text
Web
Web
Web

↓

Web
```

---

# Kubernetes Responsibilities

According to the notes, Kubernetes manages:

- Deployment
- Container Orchestration
- Scaling Up
- Scaling Down
- High Availability
- Node Management

---

# Commands

> **No Kubernetes (`kubectl`) commands are introduced in these notes yet.**
>
> Commands will be added starting from the sections where they appear in the PDF.

---

# Quick Revision

```text
Container Orchestration

↓

Kubernetes

↓

Node

↓

Cluster

↓

Master Node

↓

Worker Nodes

↓

Deployment

↓

Scaling

↓

High Availability
```

---

# Summary

- Kubernetes is a Container Orchestration Technology.
- A Node is a machine where containers run.
- A Cluster is a group of Nodes.
- The Master Node manages Worker Nodes.
- Kubernetes provides High Availability.
- Kubernetes automatically performs Scale Up and Scale Down operations.