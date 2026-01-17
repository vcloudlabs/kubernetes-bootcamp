# Lab: Pod PriorityClass and Preemption

## Difficulty
Intermediate

## Estimated Time
15–20 minutes

---

## Objective

In this lab, you will:

- Create Kubernetes **PriorityClass** objects
- Deploy pods with different priorities
- Simulate **resource pressure**
- Observe **pod preemption** in action
- Understand how the scheduler makes eviction decisions

This lab demonstrates real Kubernetes scheduling behavior under constrained resources.

---

## Prerequisites

- A running Kubernetes cluster (Minikube recommended)
- kubectl configured and working
- Cluster with **limited CPU and memory**

> ⚠️ This lab works best on a resource-constrained cluster (for example: Minikube with 2 CPUs and 2–4GB memory).

---

## Step 1: Verify Node Capacity

```bash
kubectl get nodes
kubectl describe node minikube
```

Look at:
- Capacity
- Allocatable

These values determine scheduling and preemption behavior.

---

## Step 2: Create PriorityClass Objects

### low-priority.yaml
```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: low-priority
value: 1000
globalDefault: false
description: "Low priority workloads"
```

### high-priority.yaml
```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 100000
globalDefault: false
description: "High priority workloads"
```

Apply:
```bash
kubectl apply -f low-priority.yaml
kubectl apply -f high-priority.yaml
```

Verify:
```bash
kubectl get priorityclass
```

---

## Step 3: Deploy Low-Priority Pods

### low-priority-pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: low-priority-pod
spec:
  priorityClassName: low-priority
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        cpu: "500m"
        memory: "512Mi"
      limits:
        cpu: "500m"
        memory: "512Mi"
```

```bash
kubectl apply -f low-priority-pod.yaml
kubectl get pods
```

Deploy multiple copies if needed to exhaust resources.

---

## Step 4: Deploy a High-Priority Pod

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
      limits:
        cpu: "500m"
        memory: "512Mi"
```

```bash
kubectl apply -f high-priority-pod.yaml
```

---

## Step 5: Observe Preemption

```bash
kubectl get pods -w
```

Expected:
- Low-priority pod(s) evicted
- High-priority pod scheduled and running

Check events:
```bash
kubectl describe pod high-priority-pod
```

---

## Key Learnings

- Preemption happens only when required
- Only lower-priority pods are evicted
- Requests (not limits) drive scheduling
- Priority affects scheduling order

---

## Common Issues

- No preemption → cluster has free resources
- PriorityClass missing or typo
- Requests too small to trigger pressure

---

## Cleanup

```bash
kubectl delete pod low-priority-pod high-priority-pod
kubectl delete priorityclass low-priority high-priority
```

---

## Why This Matters for CKA

Priority & Preemption is a core scheduling concept frequently tested in real troubleshooting scenarios.

Mastering this lab builds real scheduler intuition.

