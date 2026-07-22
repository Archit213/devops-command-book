# 🚀 Deployments

A **Deployment** is a higher-level Kubernetes object that manages ReplicaSets and Pods.

It provides an easy way to deploy applications, perform rolling updates, roll back changes, and scale applications.

A Deployment automatically creates and manages a ReplicaSet.

---

# Why Deployments?

Suppose an application is already running with 5 Pods.

Now you want to:

- Update the application version
- Roll back if the update fails
- Scale the application
- Perform updates without downtime

A ReplicaSet cannot efficiently manage application updates.

A Deployment solves these problems.

---

# Deployment Architecture

```text
                    Deployment
                         │
                         ▼
                  ReplicaSet
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
        Pod-1          Pod-2          Pod-3
```

Deployment never creates Pods directly.

Instead,

Deployment

↓

ReplicaSet

↓

Pods

---

# Responsibilities of Deployment

- Deploy applications
- Scale applications
- Rolling Updates
- Rollback
- Self-healing
- Manage ReplicaSets

---

# Deployment Workflow

```text
Deployment

↓

ReplicaSet

↓

Pods

↓

Application Running
```

---

# Deployment YAML

```yaml
apiVersion: apps/v1

kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:

    metadata:
      labels:
        app: nginx

    spec:
      containers:

      - name: nginx

        image: nginx:latest
```

---

# YAML Breakdown

| Field | Description |
|--------|-------------|
| apiVersion | Kubernetes Apps API |
| kind | Deployment resource |
| metadata | Deployment information |
| replicas | Desired number of Pods |
| selector | Select Pods |
| template | Pod Template |
| containers | Container specification |
| image | Docker image |

---

# Deployment Lifecycle

```text
Create Deployment

↓

ReplicaSet Created

↓

Pods Created

↓

Application Running

↓

Update Image

↓

Rolling Update

↓

New ReplicaSet

↓

Old ReplicaSet Removed
```

---

# Rolling Update

A Rolling Update replaces Pods one by one.

```text
Version 1

Pod
Pod
Pod

↓

Rolling Update

↓

Pod(v2)

Pod(v1)

Pod(v1)

↓

Pod(v2)

Pod(v2)

Pod(v1)

↓

Pod(v2)

Pod(v2)

Pod(v2)
```

Advantages

- Zero downtime
- Controlled updates
- Easy rollback

---

# Rollback

If a deployment fails,

Kubernetes restores the previous ReplicaSet.

```text
Version 2

↓

Application Failure

↓

Rollback

↓

Version 1 Restored
```

---

# Commands

| Command | Description |
|----------|-------------|
| `kubectl get deployments` | List Deployments |
| `kubectl get deploy` | List Deployments |
| `kubectl describe deployment nginx-deployment` | Deployment details |
| `kubectl apply -f deployment.yaml` | Create Deployment |
| `kubectl create deployment nginx --image=nginx` | Create Deployment using CLI |
| `kubectl scale deployment nginx-deployment --replicas=5` | Scale Deployment |
| `kubectl rollout status deployment/nginx-deployment` | Deployment status |
| `kubectl rollout history deployment/nginx-deployment` | View rollout history |
| `kubectl rollout undo deployment/nginx-deployment` | Rollback Deployment |
| `kubectl set image deployment/nginx-deployment nginx=nginx:1.27` | Update image |
| `kubectl delete deployment nginx-deployment` | Delete Deployment |

---

# Practical Implementation

## Create Deployment using YAML

```bash
kubectl apply -f deployment.yaml
```

### Expected Output

```text
deployment.apps/nginx-deployment created
```

---

## Create Deployment using CLI

```bash
kubectl create deployment nginx --image=nginx
```

### Expected Output

```text
deployment.apps/nginx created
```

---

## View Deployments

```bash
kubectl get deployments
```

### Expected Output

```text
NAME               READY   UP-TO-DATE   AVAILABLE
nginx-deployment   3/3     3            3
```

---

## Describe Deployment

```bash
kubectl describe deployment nginx-deployment
```

### Expected Output

```text
Name: nginx-deployment

Replicas: 3 desired | 3 updated | 3 available
```

---

## Scale Deployment

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

### Expected Output

```text
deployment.apps/nginx-deployment scaled
```

---

## Check Rollout Status

```bash
kubectl rollout status deployment/nginx-deployment
```

### Expected Output

```text
deployment "nginx-deployment" successfully rolled out
```

---

## View Rollout History

```bash
kubectl rollout history deployment/nginx-deployment
```

### Expected Output

```text
REVISION

1

2
```

---

## Update Container Image

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.27
```

### Expected Output

```text
deployment.apps/nginx-deployment image updated
```

---

## Rollback Deployment

```bash
kubectl rollout undo deployment/nginx-deployment
```

### Expected Output

```text
deployment.apps/nginx-deployment rolled back
```

---

## Delete Deployment

```bash
kubectl delete deployment nginx-deployment
```

### Expected Output

```text
deployment.apps "nginx-deployment" deleted
```

---

# Deployment vs ReplicaSet

| ReplicaSet | Deployment |
|-------------|------------|
| Maintains Pod replicas | Manages ReplicaSets |
| Self-healing | Self-healing |
| Scaling | Scaling |
| No rolling updates | Supports rolling updates |
| No rollback | Supports rollback |
| Basic controller | Higher-level controller |

---

# Quick Revision

```text
Deployment

↓

ReplicaSet

↓

Pods

↓

Rolling Update

↓

Rollback

↓

Scaling

↓

High Availability
```

---

# Summary

- Deployment is the recommended way to deploy applications in Kubernetes.
- It manages ReplicaSets and Pods automatically.
- Supports rolling updates with minimal downtime.
- Supports rollback to previous versions.
- Allows easy scaling of applications.
- Provides declarative application management.