# 🚀 Kubernetes Hands-On Lab (Minikube + kind)

> Practical Kubernetes implementation covering Pods, Deployments, Services, Scaling, Rolling Updates, and Multi-Node Cluster simulation.

---

## 📌 Project Overview

This repository demonstrates hands-on Kubernetes implementation using:

- 🔹 Minikube (Single-node cluster)
- 🔹 kind (Multi-node cluster using Docker)

This project covers:

- Cluster setup
- Node management
- Pod lifecycle
- Deployments
- Services
- Scaling
- Rolling updates
- Imperative vs Declarative resource creation

---

## ❓ Why Kubernetes?

Docker runs containers.  
Kubernetes manages containers at scale.

Kubernetes provides:

- Automatic scheduling
- Self-healing
- Horizontal scaling
- Rolling updates & rollbacks
- Service discovery
- Load balancing
- Multi-node cluster management

---

# 🏗️ Basic Kubernetes Architecture (Implemented Here)

Cluster = Control Plane + Worker Node(s)

Core Components Demonstrated:

- Node → Machine running workloads
- Pod → Smallest deployable unit
- Deployment → Manages replicas
- Service → Network abstraction layer

---

# 🛠 Tools Used

| Tool | Purpose |
|------|----------|
| kubectl | CLI to interact with cluster |
| Minikube | Single-node local cluster |
| kind | Multi-node Kubernetes in Docker |
| Docker | Container runtime |

---

# 📂 Repository Structure

```
.
├── pod.yaml
├── pod2.yaml
├── deploy.yaml
├── config.yaml
├── kind-multinode.yaml
└── README.md
```

---

# 🚀 1️⃣ Minikube Workflow (Single Node)

## Step 1: Start Cluster

```bash
minikube start
```

Verify:

```bash
kubectl cluster-info
kubectl get nodes
```

Expected Output:

```
minikube   Ready   control-plane
```

---

## Step 2: Imperative Pod Creation

```bash
kubectl run nginx --image=nginx --port=80
kubectl get pods
```

Expose Pod:

```bash
kubectl expose pod nginx --type=NodePort --port=80
minikube service nginx --url
```

---

## Step 3: Declarative Deployment

Apply YAML:

```bash
kubectl apply -f deploy.yaml
```

Check Resources:

```bash
kubectl get deployments
kubectl get pods
kubectl get svc
```

---

## Step 4: Scale Deployment

```bash
kubectl scale deployment/nginx-deploy --replicas=3
```

---

## Step 5: Rolling Update

```bash
kubectl set image deployment/nginx-deploy nginx=nginx:1.19
kubectl rollout status deployment/nginx-deploy
```

---

## Cleanup

```bash
kubectl delete -f deploy.yaml
minikube delete
```

---

# 🚀 2️⃣ kind Workflow (Multi-Node Cluster)

## Why kind?

- Lightweight
- Fast cluster setup
- Simulates production-like multi-node architecture
- CI/CD friendly

---

# 🖥️ Multi-Node Configuration
First ensure that your docker desktop is running. In kind one docker container is one node in kubernetes.

First practice basic commands:

```bash

kind create cluster --name my-cluster     # Create a cluster (default: single-node)
                                         # To create multi-node cluster, use config file

kind get clusters                        # List all existing clusters

kind delete cluster --name my-cluster    # Delete a specific cluster

kubectl get nodes                        # View cluster nodes
```

---

Create file: `kind-multinode.yaml`

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

---

## Create Multi-Node Cluster

```bash
kind create cluster --name multi --config kind-multinode.yaml
```

Verify:

```bash
kubectl get nodes
```

Expected Output:

```
multi-control-plane   Ready
multi-worker          Ready
multi-worker2         Ready
```

---

## Deploy Application

```bash
kubectl apply -f deploy.yaml
kubectl get pods -o wide
```

Pods will be distributed across worker nodes.

---

## Port Forward

```bash
kubectl port-forward svc/nginx-svc 8080:80
```

Access:

```
http://localhost:8080
```

---

## Delete Cluster

```bash
kind delete cluster --name multi
```

---

# 📜 Example Deployment File (deploy.yaml)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 2
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
          image: nginx:1.21
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: NodePort
```

---

# 🔎 Essential kubectl Commands

```bash
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get svc
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/sh
kubectl apply -f file.yaml
kubectl delete -f file.yaml
kubectl scale deployment/<name> --replicas=N
kubectl rollout status deployment/<name>
kubectl port-forward svc/<name> 8080:80
```

---

# 📊 What This Project Demonstrates

- Cluster creation (Minikube & kind)
- Multi-node architecture simulation
- Pod lifecycle management
- Deployment strategies
- Service networking
- Horizontal scaling
- Rolling updates
- Imperative & Declarative workflows

---

# 🎯 Skills Demonstrated

- Kubernetes fundamentals
- Multi-node cluster configuration
- YAML-based infrastructure
- Container orchestration
- Service exposure techniques
- Deployment management
- CLI-based troubleshooting

---

# 📌 Future Improvements

- Ingress Controller
- ConfigMaps & Secrets
- Persistent Volumes
- Helm integration
- CI/CD pipeline using kind

---

# 👨‍💻 Author

**Aqeel Saeed**  
BS Software Engineering  
Cloud & Containerization Enthusiast