# Pod Priority & Preemption

This module covers **Pod Priority and Preemption**, a core Kubernetes **scheduling concept** that determines **which pods get to run when cluster resources are scarce**.

It is an important topic for:
- Kubernetes administrators
- SRE / Platform engineers
- **CKA exam candidates**

---

## 📌 What is Pod Priority?

Pod Priority allows you to assign an **integer priority value** to pods using a `PriorityClass`.

When multiple pods compete for limited resources:
- Pods with **higher priority** are scheduled first
- Lower-priority pods may be **preempted (evicted)** if required

---

## 📌 What is Preemption?

Preemption is the process where the Kubernetes scheduler:
- **Terminates lower-priority pods**
- To make room for **higher-priority pods**
- Only when no other scheduling option exists

Important characteristics:
- Happens **during scheduling**
- Works at the **pod level**
- Evicts the **minimum number of pods required**
- Based on **resource requests**, not limits

---

## 🧠 Why This Matters (Real World)

In real clusters:
- Critical workloads (API servers, controllers, system jobs) must always run
- Best-effort or batch workloads should yield under pressure
- Multi-tenant clusters rely heavily on priority and preemption

This is also how Kubernetes protects **system-critical components**.

---

## 🧪 Hands-on Lab

👉 **Lab:** [Click Here - demo-lab.md](demo-lab.md)  
In this lab, you will:
- Start a resource-constrained Minikube cluster
- Create PriorityClasses
- Deploy a low-priority **Deployment (3 replicas)**
- Deploy a high-priority pod
- Observe real pod preemption behavior

This lab is **CKA-aligned** and mirrors production scenarios.

---

## 🎥 YouTube Demo

📺 **Video:** *Pod Priority & Preemption Explained with Demo*  
🔗 Link: *(https://www.youtube.com/watch?v=02cbdHB1HQk)*

---

## 📝 Blog Reference

📖 **Blog:** *Understanding Pod Priority & Preemption in Kubernetes*  
🔗 Link: *(https://vcloudlabs.medium.com/kubernetes-pod-priority-preemption-making-sure-the-right-workloads-run-first-8efb2c962af4)*

The blog explains:
- Internal scheduler flow
- When preemption happens (and when it doesn’t)
- Practical use cases and pitfalls

---

## 📚 Official Kubernetes Documentation

Use these as the **source of truth**:

- Pod Priority & Preemption  
  https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/

- Scheduling Overview  
  https://kubernetes.io/docs/concepts/scheduling-eviction/

- PriorityClass API Reference  
  https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/priority-class-v1/

---

## ⚠️ Common Pitfalls (CKA Tips)

- PriorityClass created **after** pod → ignored
- Cluster has enough free resources → no preemption
- Requests too small → scheduler has no reason to evict
- Forgetting that controllers recreate evicted pods

---

## 🧩 Related Topics

You should also study:
- Resource requests & limits
- Taints and tolerations
- PodDisruptionBudgets
- `preemptionPolicy: Never`

These topics together form a complete **scheduling mental model**.

---

## 🏷 vcloudlabs Note

This module is part of the **kubernetes-bootcamp** by **vcloudlabs**.

vcloudlabs focuses on:
- Learning by doing
- Real-world Kubernetes behavior
- Exam-oriented understanding without shortcuts

---

## Next Steps

After completing this module:
- Try modifying resource requests
- Experiment with different priority values
- Add PodDisruptionBudgets
- Observe scheduler events using `kubectl get events`

Continue learning with **Kubernetes Bootcamp** 🚀
