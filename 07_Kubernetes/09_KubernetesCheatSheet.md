# ☸️ Kubernetes kubectl Cheat Sheet

> A quick reference guide for the most commonly used `kubectl` commands covered in the Kubernetes notes.

---

# Cluster Information

| Command | Description |
|----------|-------------|
| `kubectl version` | Display client and server Kubernetes versions |
| `kubectl cluster-info` | Display cluster information |
| `kubectl config view` | View kubeconfig configuration |
| `kubectl config current-context` | Show the current Kubernetes context |
| `kubectl config get-contexts` | List all available contexts |
| `kubectl config use-context <context-name>` | Switch to another Kubernetes cluster/context |

---

# Node Commands

| Command | Description |
|----------|-------------|
| `kubectl get nodes` | List all worker nodes |
| `kubectl get no` | Short form for listing nodes |
| `kubectl describe node <node-name>` | Display detailed node information |
| `kubectl top node` | Show node CPU and memory usage *(Metrics Server required)* |

---

# Pod Commands

| Command | Description |
|----------|-------------|
| `kubectl run nginx --image=nginx` | Create a Pod |
| `kubectl get pods` | List Pods |
| `kubectl get pod` | Short form for Pods |
| `kubectl get pods -o wide` | Show detailed Pod information |
| `kubectl get pods --watch` | Continuously watch Pod status |
| `kubectl describe pod <pod-name>` | Display Pod details |
| `kubectl logs <pod-name>` | View Pod logs |
| `kubectl logs -f <pod-name>` | Stream Pod logs |
| `kubectl exec -it <pod-name> -- /bin/bash` | Open interactive shell |
| `kubectl delete pod <pod-name>` | Delete a Pod |

---

# ReplicaSet Commands

| Command | Description |
|----------|-------------|
| `kubectl get rs` | List ReplicaSets |
| `kubectl get replicaset` | List ReplicaSets |
| `kubectl describe rs <replicaset-name>` | Display ReplicaSet details |
| `kubectl apply/create -f replicaset.yaml` | Create ReplicaSet |
| `kubectl edit rs <replicaset-name>` | Edit ReplicaSet |
| `kubectl scale rs <replicaset-name> --replicas=<count>` | Scale ReplicaSet |
| `kubectl delete rs <replicaset-name>` | Delete ReplicaSet |

---

# Deployment Commands

| Command | Description |
|----------|-------------|
| `kubectl get deployments` | List Deployments |
| `kubectl get deploy` | Short form for Deployments |
| `kubectl describe deployment <deployment-name>` | Display Deployment details |
| `kubectl create deployment <name> --image=<image>` | Create Deployment |
| `kubectl apply -f deployment.yaml` | Create Deployment using YAML |
| `kubectl edit deployment <deployment-name>` | Edit Deployment |
| `kubectl scale deployment <deployment-name> --replicas=<count>` | Scale Deployment |
| `kubectl delete deployment <deployment-name>` | Delete Deployment |

---

# Rollout Commands

| Command | Description |
|----------|-------------|
| `kubectl rollout status deployment/<deployment-name>` | View rollout status |
| `kubectl rollout history deployment/<deployment-name>` | View rollout history |
| `kubectl rollout undo deployment/<deployment-name>` | Roll back Deployment |
| `kubectl rollout restart deployment/<deployment-name>` | Restart Deployment |

---

# Image Update Commands

| Command | Description |
|----------|-------------|
| `kubectl set image deployment/<deployment> <container>=<image>` | Update container image |
| `kubectl set image deployment/nginx nginx=nginx:1.27` | Example image update |

---

# Service Commands

| Command | Description |
|----------|-------------|
| `kubectl get svc` | List Services |
| `kubectl get services` | List Services |
| `kubectl describe svc <service-name>` | Display Service details |
| `kubectl apply -f service.yaml` | Create Service |
| `kubectl expose deployment <deployment> --port=<port> --target-port=<port>` | Expose Deployment |
| `kubectl delete svc <service-name>` | Delete Service |

---

# Labels Commands

| Command | Description |
|----------|-------------|
| `kubectl get pods --show-labels` | Display Pod labels |
| `kubectl get all --show-labels` | Display labels for all resources |
| `kubectl label pod <pod-name> app=frontend` | Add label |
| `kubectl label pod <pod-name> env=dev` | Add another label |
| `kubectl label pod <pod-name> app-` | Remove label |
| `kubectl get pods -l app=frontend` | Filter Pods using labels |

---

# Resource Inspection

| Command | Description |
|----------|-------------|
| `kubectl get all` | Display all resources |
| `kubectl describe <resource> <name>` | Display detailed resource information |
| `kubectl api-resources` | List supported resource types |
| `kubectl api-versions` | Display supported API versions |
| `kubectl explain pod` | Display Pod documentation |
| `kubectl explain deployment.spec` | Explain Deployment fields |

---

# YAML Generation Commands

| Command | Description |
|----------|-------------|
| `kubectl run nginx --image=nginx --dry-run=client -o yaml` | Generate Pod YAML |
| `kubectl create deployment nginx --image=nginx --dry-run=client -o yaml` | Generate Deployment YAML |
| `kubectl create namespace dev --dry-run=client -o yaml` | Generate Namespace YAML |

---

# Apply & Delete Resources

| Command | Description |
|----------|-------------|
| `kubectl apply -f <file>.yaml` | Create or update resources |
| `kubectl create -f <file>.yaml` | Create resources |
| `kubectl replace -f <file>.yaml` | Replace resource |
| `kubectl delete -f <file>.yaml` | Delete resources from YAML |

---

# Scaling Commands

| Command | Description |
|----------|-------------|
| `kubectl scale deployment <name> --replicas=<count>` | Scale Deployment |
| `kubectl scale rs <name> --replicas=<count>` | Scale ReplicaSet |

---

# Logs & Debugging

| Command | Description |
|----------|-------------|
| `kubectl logs <pod-name>` | View Pod logs |
| `kubectl logs -f <pod-name>` | Follow logs in real time |
| `kubectl describe pod <pod-name>` | Troubleshoot Pod |
| `kubectl exec -it <pod-name> -- /bin/bash` | Access Pod shell |

---

# Resource Monitoring

| Command | Description |
|----------|-------------|
| `kubectl top pod` | Show Pod resource usage *(Metrics Server required)* |
| `kubectl top node` | Show Node resource usage *(Metrics Server required)* |

---

# Common Short Names

| Full Resource | Short Name |
|---------------|------------|
| Pods | `po` |
| Nodes | `no` |
| Services | `svc` |
| Deployments | `deploy` |
| ReplicaSets | `rs` |
| Namespaces | `ns` |
| ConfigMaps | `cm` |
| PersistentVolumes | `pv` |
| PersistentVolumeClaims | `pvc` |

---

# Most Frequently Used Commands

```bash
kubectl get pods

kubectl get all

kubectl get nodes

kubectl get deployments

kubectl get svc

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl exec -it <pod-name> -- /bin/bash

kubectl apply -f deployment.yaml

kubectl delete pod <pod-name>

kubectl scale deployment nginx --replicas=5

kubectl rollout status deployment/nginx

kubectl rollout undo deployment/nginx

kubectl set image deployment/nginx nginx=nginx:1.27
```

---

# Revision Flow

```text
Cluster
   │
Nodes
   │
Namespaces
   │
Pods
   │
ReplicaSets
   │
Deployments
   │
Services
   │
Labels & Selectors
   │
Scaling
   │
Rollouts
   │
Troubleshooting
```

---
