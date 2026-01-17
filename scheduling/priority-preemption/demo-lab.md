# Lab: Pod PriorityClass and Preemption

## Difficulty
Intermediate

## Estimated Time
20 minutes

---

## Objective

In this lab, you will:

- Start a **resource-constrained Kubernetes cluster using Minikube**
- Create Kubernetes **PriorityClass** objects
- Deploy a **low-priority Deployment with multiple replicas**
- Deploy a **high-priority Pod**
- Observe **pod preemption** under resource pressure
- Understand how Kubernetes evicts lower-priority pods during scheduling

This lab mirrors real-world and CKA-style scheduling scenarios.

---

## Prerequisites

- Minikube installed
- kubectl installed and configured
- Virtualization support enabled

---

## Step 1: Start Minikube with Resource Constraints

```bash
minikube stop
minikube delete
minikube start --cpus=2 --memory=4096
```

---

## Step 2: Verify Node Capacity

```bash
kubectl get nodes
kubectl describe node minikube
```

---

## Step 3: Create PriorityClass Objects

### low-priority.yaml
```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: low-priority
value: 1000
```

### high-priority.yaml
```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 100000
```

```bash
kubectl apply -f low-priority.yaml
kubectl apply -f high-priority.yaml
```

---

## Step 4: Deploy Low-Priority Deployment (3 Replicas)

### low-priority-deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: low-priority-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: low-priority
  template:
    metadata:
      labels:
        app: low-priority
    spec:
      priorityClassName: low-priority
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: "500m"
            memory: "512Mi"
```

```bash
kubectl apply -f low-priority-deployment.yaml
kubectl get pods
```

Increase the replica counts if needed to exhaust the resource and **one of the low priority replica pod goes into pending state.**

---

## Step 5: Deploy High-Priority Pod

### high-priority-pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: high-priority-pod
spec:
  priorityClassName: high-priority
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        cpu: "500m"
        memory: "512Mi"
```

```bash
kubectl apply -f high-priority-pod.yaml
```

---

## Step 6: Observe Preemption

```bash
kubectl get pods -w
```

Expected:
- One or more low-priority pods evicted
- High-priority pod running

---

## Cleanup

```bash
kubectl delete deployment low-priority-deployment
kubectl delete pod high-priority-pod
kubectl delete priorityclass low-priority high-priority
minikube stop
```

---

## Why This Matters

Most real workloads run as Deployments. Preemption always happens at the **pod level**.

Understanding this is critical for CKA and production troubleshooting.
