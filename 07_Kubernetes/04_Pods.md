# 🚀 Pods

A **Pod** is the **smallest deployable unit** in Kubernetes.

A Pod is the basic execution unit that runs one or more containers.

In most real-world scenarios, a Pod contains **one application container**.

---

# Why Do We Need Pods?

Kubernetes does not deploy containers directly.

Instead, every container runs **inside a Pod**.

```text
Container
      ❌
Cannot be deployed directly

        │

        ▼

+----------------+
|      Pod       |
|                |
|  +----------+  |
|  |Container |  |
|  +----------+  |
+----------------+

        │

Worker Node
```

---

# Pod Architecture

```text
               Worker Node

      +-------------------------+
      |         Pod             |
      |                         |
      |   +-----------------+   |
      |   |   Container     |   |
      |   +-----------------+   |
      +-------------------------+
```

A Pod acts as a wrapper around one or more containers.

---

# One Container per Pod

Most Kubernetes applications follow:

```text
1 Pod

↓

1 Container
```

Example

```text
Pod

↓

Nginx Container
```

---

# Multiple Containers in a Pod

Sometimes multiple tightly coupled containers share the same Pod.

Example

```text
+-----------------------------+
|            Pod              |
|                             |
| +---------+  +-----------+  |
| |  Nginx  |  | Log Agent |  |
| +---------+  +-----------+  |
+-----------------------------+
```

Both containers:

- Share storage
- Share networking
- Communicate using localhost

---

# Pod Lifecycle

```text
Create Pod

↓

Running

↓

Succeeded

or

Failed

↓

Deleted
```

Pods are **ephemeral**.

If a Pod fails, Kubernetes creates another Pod instead of repairing the old one.

---

# Creating a Pod

Example Pod YAML

```yaml
apiVersion: v1

kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
  - name: nginx
    image: nginx
```

---

# YAML Breakdown

| Field | Description |
|--------|-------------|
| apiVersion | Kubernetes API version |
| kind | Resource type |
| metadata | Information about the object |
| name | Pod name |
| spec | Desired state |
| containers | List of containers |
| image | Docker image |

---

# Commands

| Command | Description |
|----------|-------------|
| `kubectl run nginx --image=nginx` | Create a Pod |
| `kubectl get pods` | List Pods |
| `kubectl get pod` | List Pods |
| `kubectl describe pod nginx` | Display Pod details |
| `kubectl logs nginx` | View Pod logs |
| `kubectl delete pod nginx` | Delete a Pod |
| `kubectl get pods -o wide` | Show additional Pod information |
| `kubectl get pods --watch` | Continuously monitor Pods |

---

# Practical Implementation

## Create a Pod

### Use Case

Deploy a simple Nginx web server.

### Command

```bash
kubectl run nginx --image=nginx
```

### Expected Output

```text
pod/nginx created
```

---

## List Pods

### Command

```bash
kubectl get pods
```

### Expected Output

```text
NAME      READY   STATUS    RESTARTS   AGE
nginx     1/1     Running   0          30s
```

---

## Show Detailed Pod Information

### Command

```bash
kubectl describe pod nginx
```

### Expected Output

```text
Name: nginx

Namespace: default

Node: worker-01

Status: Running

IP: 10.244.0.8

Containers:
  nginx
```

---

## View Pod Logs

### Command

```bash
kubectl logs nginx
```

### Expected Output

```text
172.17.0.1 GET / HTTP/1.1 200
172.17.0.1 GET /favicon.ico 404
```

---

## Delete a Pod

### Command

```bash
kubectl delete pod nginx
```

### Expected Output

```text
pod "nginx" deleted
```

---

## View Extended Pod Information

### Command

```bash
kubectl get pods -o wide
```

### Expected Output

```text
NAME    READY   STATUS    IP           NODE
nginx   1/1     Running   10.244.0.8   worker-01
```

---

## Watch Pods in Real Time

### Command

```bash
kubectl get pods --watch
```

### Expected Output

```text
NAME      READY   STATUS    AGE
nginx     1/1     Running   35s
```

Press **Ctrl + C** to stop watching.

---

# Useful Pod Operations

```text
Create

↓

View

↓

Describe

↓

Logs

↓

Delete
```

---

# Quick Revision

```text
Pod

↓

Smallest Deployable Unit

↓

Contains One or More Containers

↓

Runs on Worker Node

↓

Managed by ReplicaSet

↓

Created using kubectl
```

---

# Summary

- A Pod is the smallest deployable object in Kubernetes.
- Every container runs inside a Pod.
- A Pod can contain one or multiple containers.
- Pods are temporary and can be recreated by Kubernetes.
- `kubectl` is used to create, inspect, monitor, and delete Pods.