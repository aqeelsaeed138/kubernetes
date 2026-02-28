# Kubernetes Hands-On (Minikube + kind)

## 📌 Introduction

This repository demonstrates my hands-on learning of **Kubernetes** using:

- Minikube (Local single-node cluster)
- kind (Kubernetes in Docker)

Kubernetes is a container orchestration platform used to deploy, manage, scale, and monitor containerized applications.

---

## ❓ Why We Need Kubernetes

Docker can run containers, but in production we need:

- Automatic scaling
- Self-healing (restart failed containers)
- Load balancing
- Rolling updates
- Service discovery
- Multi-node cluster management

Kubernetes solves all these problems.

---

# 🛠 Tools Used

## 1️⃣ Minikube

Minikube runs a single-node Kubernetes cluster locally.

### Advantages
- Beginner friendly
- Built-in dashboard
- Easy service access
- Supports VM & Docker drivers

---

## 2️⃣ kind (Kubernetes in Docker)

kind runs Kubernetes clusters inside Docker containers.

### Advantages
- Very lightweight
- Fast cluster creation
- Ideal for CI/CD
- Can simulate multi-node clusters

---

# 🧱 Basic Kubernetes Architecture (Simple)

Cluster = Control Plane + Worker Node(s)

Main Components:

- Node → Machine that runs Pods
- Pod → Smallest deployable unit
- Deployment → Manages multiple Pods
- Service → Exposes Pods to network

---

# 🚀 COMPLETE WORKFLOW — MINIKUBE

---

## Step 1: Start Cluster

```bash
minikube start