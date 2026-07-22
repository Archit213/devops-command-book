# ⚙️ Kubernetes Components

When Kubernetes is installed, several core components are installed together to manage and operate the cluster.

These components work together to deploy, schedule, monitor, and manage applications.

---

# Kubernetes Components

- API Server
- etcd
- Scheduler
- Controller Manager
- Container Runtime
- Kubelet
- kube-proxy

---

# Kubernetes Control Plane

```text
                  Kubernetes Cluster

                  ┌───────────────┐
                  │  API Server   │
                  └──────┬────────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
      Scheduler       etcd      Controller Manager
                         │
                Worker Nodes
          ┌────────────────────────────┐
          │ kubelet                    │
          │ Container Runtime          │
          │ kube-proxy                 │
          │ Pods                       │
          └────────────────────────────┘
```

---

# API Server

The **API Server** is the front-end of Kubernetes.

It receives all requests made using:

- kubectl
- REST API
- UI

Every communication inside the Kubernetes cluster passes through the API Server.

### Responsibilities

- Accept user requests
- Validate requests
- Authenticate users
- Update cluster state
- Communicate with other Kubernetes components

---

# etcd

**etcd** is a distributed key-value database.

It stores all Kubernetes cluster information.

Examples:

- Nodes
- Pods
- Deployments
- Secrets
- ConfigMaps
- Cluster configuration

Without etcd, Kubernetes cannot remember the cluster state.

---

# Scheduler

The Scheduler decides **where a Pod should run**.

It checks:

- Available CPU
- Available Memory
- Resource requests
- Node health
- Scheduling rules

Then assigns the Pod to the most suitable Worker Node.

---

# Controller Manager

The Controller Manager continuously monitors the cluster.

It ensures the **desired state** matches the **actual state**.

Example:

Desired Replicas

```text
3 Pods
```

Current State

```text
2 Pods
```

Controller Manager creates one additional Pod automatically.

---

# Container Runtime

The Container Runtime is responsible for running containers.

Examples include:

- containerd
- CRI-O

Responsibilities:

- Pull container images
- Start containers
- Stop containers
- Remove containers

---

# Kubelet

Kubelet runs on every Worker Node.

Responsibilities:

- Communicate with API Server
- Create Pods
- Monitor Pods
- Report Pod status
- Ensure containers remain healthy

---

# kube-proxy

kube-proxy runs on every Worker Node.

Responsibilities:

- Network communication
- Service networking
- Load balancing
- Pod-to-Pod communication

---

# kubectl

`kubectl` is the Kubernetes Command Line Interface (CLI).

It is used to interact with the Kubernetes API Server.

---

# Commands Mentioned

| Command | Description |
|----------|-------------|
| `kubectl get nodes` | Display all worker nodes in the cluster |
| `kubectl cluster-info` | Display Kubernetes cluster information |
| `kubectl get pods` | Display Pods in the cluster |
| `kubectl get deployments` | Display Deployments |

---

# Practical Examples

## Display Nodes

### Command

```bash
kubectl get nodes
```

### Expected Output

```text
NAME        STATUS   ROLES           AGE   VERSION
master      Ready    control-plane   10d   v1.33.0
worker-01   Ready    <none>          10d   v1.33.0
worker-02   Ready    <none>          10d   v1.33.0
```

---

## Display Cluster Information

### Command

```bash
kubectl cluster-info
```

### Expected Output

```text
Kubernetes control plane is running at https://192.168.1.100:6443
CoreDNS is running at https://192.168.1.100:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

---

## List Pods

### Command

```bash
kubectl get pods
```

### Expected Output

```text
NAME          READY   STATUS    RESTARTS   AGE
nginx-pod     1/1     Running   0          5m
```

---

## Display Deployments

### Command

```bash
kubectl get deployments
```

### Expected Output

```text
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
web-app   3/3     3            3           12m
```

---

# Component Summary

| Component | Purpose |
|------------|---------|
| API Server | Entry point for all Kubernetes requests |
| etcd | Cluster database |
| Scheduler | Selects the best node for Pods |
| Controller Manager | Maintains desired cluster state |
| Container Runtime | Runs containers |
| Kubelet | Node agent that manages Pods |
| kube-proxy | Networking and Service communication |

---

# Quick Revision

```text
User

↓

kubectl

↓

API Server

↓

etcd

↓

Scheduler

↓

Controller Manager

↓

Worker Node

↓

Kubelet

↓

Container Runtime

↓

Pods
```

---

# Summary

- API Server is the gateway to Kubernetes.
- etcd stores the complete cluster state.
- Scheduler decides where Pods run.
- Controller Manager keeps the cluster in its desired state.
- Kubelet manages Pods on each Worker Node.
- kube-proxy enables networking and load balancing.
- kubectl is the command-line tool used to interact with the cluster.