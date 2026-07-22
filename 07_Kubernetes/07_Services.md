# 🌐 Kubernetes Services

## What is a Service?

A **Service** is a Kubernetes object that provides a stable network endpoint for accessing one or more Pods.

Pods are **ephemeral**—they can be created, deleted, or recreated at any time. Since Pod IP addresses change, applications cannot reliably communicate using Pod IPs directly.

A Service solves this problem by providing a **fixed IP address** and **DNS name**.

---

# Why Do We Need Services?

Suppose an application is running in a Pod.

```text
Client

↓

Pod

(IP = 10.244.0.15)
```

If the Pod is deleted,

```text
Pod Deleted

↓

New Pod Created

↓

New IP Assigned

↓

Application Becomes Unreachable
```

Service provides a permanent endpoint.

```text
Client

↓

Service

↓

Pod 1

Pod 2

Pod 3
```

Even if Pods change, the Service continues to route traffic correctly.

---

# Service Architecture

```text
                    Client
                       │
                       ▼
                Kubernetes Service
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        Pod-1        Pod-2        Pod-3
```

The Service automatically forwards requests to healthy Pods.

---

# Types of Kubernetes Services

## 1. ClusterIP

Default Service type.

Accessible **only within the Kubernetes Cluster**.

```text
Pod A

↓

ClusterIP Service

↓

Pod B
```

Use Cases

- Backend APIs
- Databases
- Internal communication

---

## 2. NodePort

Exposes the application outside the cluster using a Node IP and Port.

```text
Internet

↓

Node IP : 30080

↓

NodePort Service

↓

Pods
```

Default NodePort Range

```text
30000 - 32767
```

---

## 3. LoadBalancer

Used in Cloud environments.

Creates an external cloud load balancer.

```text
Internet

↓

Cloud Load Balancer

↓

Service

↓

Pods
```

Commonly used on:

- AWS
- Azure
- Google Cloud

---

# Service YAML Example

```yaml
apiVersion: v1

kind: Service

metadata:
  name: nginx-service

spec:

  selector:
    app: nginx

  ports:

  - protocol: TCP

    port: 80

    targetPort: 80

  type: ClusterIP
```

---

# YAML Breakdown

| Field | Description |
|--------|-------------|
| apiVersion | Kubernetes API version |
| kind | Service |
| metadata | Object information |
| selector | Selects matching Pods |
| ports | Service ports |
| port | Service Port |
| targetPort | Container Port |
| type | Service Type |

---

# How Services Work

```text
Service

↓

Find Pods using Labels

↓

Forward Requests

↓

Load Balance Traffic
```

The Service uses **Selectors** to determine which Pods should receive incoming requests.

---

# Commands

| Command | Description |
|----------|-------------|
| `kubectl get svc` | List Services |
| `kubectl get services` | List Services |
| `kubectl describe svc nginx-service` | Display Service details |
| `kubectl apply -f service.yaml` | Create Service |
| `kubectl expose deployment nginx --port=80 --target-port=80` | Expose Deployment as a Service |
| `kubectl delete svc nginx-service` | Delete Service |

---

# Practical Implementation

## Create Service

### Command

```bash
kubectl apply -f service.yaml
```

### Expected Output

```text
service/nginx-service created
```

---

## List Services

### Command

```bash
kubectl get svc
```

### Expected Output

```text
NAME            TYPE        CLUSTER-IP      PORT(S)
kubernetes      ClusterIP   10.96.0.1       443/TCP
nginx-service   ClusterIP   10.96.25.110    80/TCP
```

---

## Describe Service

### Command

```bash
kubectl describe svc nginx-service
```

### Expected Output

```text
Name: nginx-service

Type: ClusterIP

IP: 10.96.25.110

Selector:

app=nginx
```

---

## Expose a Deployment

### Command

```bash
kubectl expose deployment nginx \
--port=80 \
--target-port=80
```

### Expected Output

```text
service/nginx exposed
```

---

## Delete Service

### Command

```bash
kubectl delete svc nginx-service
```

### Expected Output

```text
service "nginx-service" deleted
```

---

# Service Types Comparison

| Service Type | Accessible From | Typical Use |
|---------------|-----------------|-------------|
| ClusterIP | Inside Cluster | Internal communication |
| NodePort | Outside Cluster | Testing and development |
| LoadBalancer | Internet | Production workloads |

---

# Best Practices

- Use **ClusterIP** for internal applications.
- Use **NodePort** mainly for testing or lab environments.
- Use **LoadBalancer** in cloud environments for external access.
- Select Pods using consistent labels.
- Keep Service definitions separate from Deployment YAML where practical.

---

# Quick Revision

```text
Pods

↓

Dynamic IP

↓

Service

↓

Stable IP

↓

ClusterIP

↓

NodePort

↓

LoadBalancer
```

---

# Summary

- A Service provides a stable network endpoint for Pods.
- Services route traffic using Pod labels and selectors.
- ClusterIP is the default service type.
- NodePort exposes applications outside the cluster using a node port.
- LoadBalancer integrates with cloud providers to expose applications to the Internet.
- Services continue working even if underlying Pods are recreated.