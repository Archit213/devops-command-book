# 🏷️ Labels and Selectors

## Introduction

Labels are **key-value pairs** attached to Kubernetes objects such as Pods, ReplicaSets, Deployments, and Services.

Selectors use these labels to identify and manage Kubernetes resources.

Labels and Selectors are one of the core concepts in Kubernetes because they establish relationships between different objects.

---

# Why Do We Need Labels?

Suppose a cluster contains multiple applications.

```text
Kubernetes Cluster

│

├── Frontend Pods

├── Backend Pods

├── Database Pods
```

Without labels, Kubernetes cannot determine which Pods belong to which application.

Labels solve this problem.

---

# Label

A label is a **key-value pair** assigned to a Kubernetes object.

Example

```yaml
labels:
  app: nginx
  env: production
  tier: frontend
```

Here,

| Key | Value |
|------|-------|
| app | nginx |
| env | production |
| tier | frontend |

---

# Selector

A Selector searches for resources having matching labels.

Example

```yaml
selector:
  matchLabels:
    app: nginx
```

Only Pods having

```yaml
labels:
  app: nginx
```

will be selected.

---

# Labels and Selectors Relationship

```text
                 Service

             app = nginx

                   │

        ┌──────────┴──────────┐

        ▼                     ▼

     Pod 1                 Pod 2

labels:                  labels:

app=nginx               app=nginx
```

Pods having different labels are ignored.

---

# Another Example

Pods

```text
Pod A

app=frontend
```

```text
Pod B

app=frontend
```

```text
Pod C

app=database
```

Selector

```yaml
matchLabels:
  app: frontend
```

Selected Pods

```text
Pod A

Pod B
```

Ignored

```text
Pod C
```

---

# Labels in Pod YAML

```yaml
apiVersion: v1

kind: Pod

metadata:

  name: nginx-pod

  labels:

    app: nginx

    tier: frontend

spec:

  containers:

  - name: nginx

    image: nginx
```

---

# Labels in Deployment YAML

```yaml
spec:

  selector:

    matchLabels:

      app: nginx

  template:

    metadata:

      labels:

        app: nginx
```

The Deployment creates Pods having the same labels.

---

# Where Labels are Used

Labels are commonly used by:

- ReplicaSets
- Deployments
- Services
- Network Policies
- Monitoring Tools

---

# Commands

| Command | Description |
|----------|-------------|
| `kubectl get pods --show-labels` | Display Pods along with labels |
| `kubectl label pod nginx app=frontend` | Add a label to a Pod |
| `kubectl label pod nginx env=dev` | Add another label |
| `kubectl label pod nginx app-` | Remove a label |
| `kubectl get pods -l app=frontend` | List Pods matching a label |
| `kubectl describe pod nginx` | View Pod labels |
| `kubectl get all --show-labels` | Show labels for all resources |

---

# Practical Implementation

## View Labels

### Command

```bash
kubectl get pods --show-labels
```

### Expected Output

```text
NAME      READY   STATUS    LABELS

nginx     1/1     Running   app=nginx,tier=frontend
```

---

## Add Label

### Command

```bash
kubectl label pod nginx app=frontend
```

### Expected Output

```text
pod/nginx labeled
```

---

## Add Another Label

### Command

```bash
kubectl label pod nginx env=dev
```

### Expected Output

```text
pod/nginx labeled
```

---

## Remove Label

### Command

```bash
kubectl label pod nginx app-
```

### Expected Output

```text
pod/nginx unlabeled
```

---

## Filter Pods Using Labels

### Command

```bash
kubectl get pods -l app=frontend
```

### Expected Output

```text
NAME

frontend-pod-1

frontend-pod-2
```

---

## Describe Pod

### Command

```bash
kubectl describe pod nginx
```

### Expected Output

```text
Labels:

app=frontend

env=dev

tier=frontend
```

---

## Display Labels for All Resources

### Command

```bash
kubectl get all --show-labels
```

### Expected Output

```text
NAME                 LABELS

pod/nginx            app=frontend

deployment.apps/web  app=frontend
```

---

# Best Practices

- Use meaningful labels.
- Keep naming conventions consistent.
- Avoid unnecessary labels.
- Use labels to organize applications.
- Reuse labels across Deployments, ReplicaSets, Pods, and Services.

---

# Common Label Keys

```text
app

environment

tier

version

release

component
```

Example

```yaml
labels:

  app: ecommerce

  tier: backend

  environment: production

  version: v1
```

---

# Quick Revision

```text
Labels

↓

Key-Value Pair

↓

Selector

↓

matchLabels

↓

ReplicaSet

↓

Deployment

↓

Service
```

---

# Summary

- Labels are key-value pairs attached to Kubernetes resources.
- Selectors identify resources based on matching labels.
- ReplicaSets, Deployments, and Services rely on labels to manage Pods.
- Labels help organize applications and simplify resource management.
- Kubernetes provides commands to view, add, remove, and filter labels.