# 🔄 ReplicaSets

A **ReplicaSet (RS)** is a Kubernetes controller that ensures a specified number of identical Pods are running at all times.

If a Pod crashes or is deleted, the ReplicaSet automatically creates a new Pod to maintain the desired number of replicas.

---

# Why ReplicaSets?

Suppose your application is running with only one Pod.

```text
        User

          │

          ▼

      +---------+
      |  Pod 1  |
      +---------+
```

If the Pod fails,

```text
Pod Deleted

↓

Application Down ❌
```

ReplicaSet solves this problem.

```text
            ReplicaSet

                │

      ┌─────────┼─────────┐

      ▼         ▼         ▼

    Pod 1     Pod 2     Pod 3
```

If Pod 2 fails,

```text
ReplicaSet

↓

Detects Failure

↓

Creates New Pod

↓

Desired State Restored
```

---

# Desired State

ReplicaSet continuously compares:

```text
Desired Pods = 3

Actual Pods = 2

↓

Creates One New Pod

↓

Actual Pods = 3
```

This process is continuous.

---

# ReplicaSet Architecture

```text
              API Server
                   │
                   ▼
             ReplicaSet
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
     Pod-1       Pod-2       Pod-3
```

---

# ReplicaSet YAML

```yaml
apiVersion: apps/v1

kind: ReplicaSet

metadata:
  name: nginx-rs

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
        image: nginx
```

---

# YAML Breakdown

| Field | Description |
|--------|-------------|
| apiVersion | Kubernetes Apps API |
| kind | ReplicaSet resource |
| metadata | Object information |
| replicas | Desired number of Pods |
| selector | Identifies Pods managed by ReplicaSet |
| matchLabels | Labels used for matching |
| template | Pod template |
| containers | Container specification |
| image | Docker image |

---

# Labels

Labels are key-value pairs attached to Kubernetes objects.

Example

```yaml
labels:
  app: nginx
```

---

# Selectors

Selectors identify Pods that belong to a ReplicaSet.

```yaml
selector:
  matchLabels:
    app: nginx
```

ReplicaSet only manages Pods whose labels match the selector.

---

# ReplicaSet Workflow

```text
ReplicaSet

↓

Checks Running Pods

↓

Less than Desired?

↓

YES

↓

Create New Pod
```

---

# Commands

| Command | Description |
|----------|-------------|
| `kubectl get rs` | List ReplicaSets |
| `kubectl get replicaset` | List ReplicaSets |
| `kubectl describe rs nginx-rs` | Display ReplicaSet details |
| `kubectl apply -f replicaset.yaml` | Create ReplicaSet from YAML |
| `kubectl delete rs nginx-rs` | Delete ReplicaSet |
| `kubectl scale rs nginx-rs --replicas=5` | Scale ReplicaSet |
| `kubectl edit rs nginx-rs` | Edit ReplicaSet |
| `kubectl get pods` | View Pods created by ReplicaSet |

---

# Practical Implementation

## Create ReplicaSet

### Command

```bash
kubectl apply -f replicaset.yaml
```

### Expected Output

```text
replicaset.apps/nginx-rs created
```

---

## View ReplicaSets

### Command

```bash
kubectl get rs
```

### Expected Output

```text
NAME        DESIRED   CURRENT   READY
nginx-rs    3         3         3
```

---

## View ReplicaSet Details

### Command

```bash
kubectl describe rs nginx-rs
```

### Expected Output

```text
Name: nginx-rs

Replicas: 3 current / 3 desired

Pods Status:

Running 3
```

---

## Scale ReplicaSet

Increase replicas from 3 to 5.

```bash
kubectl scale rs nginx-rs --replicas=5
```

### Expected Output

```text
replicaset.apps/nginx-rs scaled
```

Verify

```bash
kubectl get rs
```

```text
NAME        DESIRED   CURRENT   READY
nginx-rs    5         5         5
```

---

## Edit ReplicaSet

```bash
kubectl edit rs nginx-rs
```

This opens the ReplicaSet manifest in the default editor.

Modify

```yaml
replicas: 3
```

to

```yaml
replicas: 6
```

Save and exit.

ReplicaSet immediately creates additional Pods.

---

## Delete ReplicaSet

```bash
kubectl delete rs nginx-rs
```

### Expected Output

```text
replicaset.apps "nginx-rs" deleted
```

---

## View Managed Pods

```bash
kubectl get pods
```

```text
NAME                      READY   STATUS
nginx-rs-jk28d            1/1     Running
nginx-rs-fg91a            1/1     Running
nginx-rs-pq37b            1/1     Running
```

---

# ReplicaSet vs Pod

| Pod | ReplicaSet |
|-----|------------|
| Runs a single Pod | Maintains multiple Pods |
| No self-healing | Self-healing |
| Manual recovery | Automatic recovery |
| No scaling | Supports scaling |

---

# Quick Revision

```text
ReplicaSet

↓

Desired Replicas

↓

Monitor Pods

↓

Pod Deleted

↓

Automatically Create New Pod

↓

Application Remains Available
```

---

# Summary

- ReplicaSet maintains a fixed number of running Pods.
- It automatically recreates failed or deleted Pods.
- Labels and Selectors determine which Pods belong to the ReplicaSet.
- ReplicaSets support scaling by increasing or decreasing the replica count.
- Common operations include creating, viewing, describing, editing, scaling, and deleting ReplicaSets.