# Kubernetes Bootcamp

**Hands-on Kubernetes labs from fundamentals to CKA-level mastery**

---

## 📌 What is Kubernetes Bootcamp?

`kubernetes-bootcamp` is a **hands-on, Kubernetes-only learning repository** designed to take you from **absolute fundamentals** to **Certified Kubernetes Administrator (CKA)–level confidence** through practical, exam-aligned labs.

This repository is:

* ✅ **100% Kubernetes-focused** (no generic DevOps noise)
* ✅ **Learning-first**, but **exam-aware**
* ✅ Built around **doing**, not just reading
* ✅ Suitable for **beginners, working engineers, SREs, and CKA aspirants**

All examples, labs, and exercises are written using **kubectl and Kubernetes YAML**, exactly the way Kubernetes is used in real systems and in the CKA exam.

---

## 🎯 Who is this for?

This bootcamp is intentionally inclusive:

* **Beginners** starting their Kubernetes journey
* **Developers** deploying workloads on Kubernetes
* **DevOps / SRE engineers** managing clusters in production
* **CKA aspirants** preparing for the exam with hands-on practice
* **Experienced engineers** looking for structured revision

If you learn best by **building, breaking, and fixing things**, this repo is for you.

---

## 🧱 How this Bootcamp is Structured

The repository is organized by **Kubernetes domains**, closely aligned with the **CKA exam syllabus** and the official Kubernetes documentation.

```text
kubernetes-bootcamp/
├── fundamentals/          # Core Kubernetes concepts
├── workloads/             # Pods, Deployments, Jobs, CronJobs
├── scheduling/            # Taints, affinity, priority & preemption
├── networking/            # Services, Ingress, NetworkPolicies
├── configuration/         # ConfigMaps, Secrets, env management
├── storage/               # Volumes, PVCs, StatefulSets
├── security/              # RBAC, ServiceAccounts, security context
├── cluster-operations/    # Upgrades, backups, node maintenance
├── troubleshooting/       # Debugging real-world failures
└── cka-mock-exams/         # Full exam-style practice scenarios
```

Each folder represents a **clear learning milestone**.

---

## 🧪 Lab Design Philosophy

Every lab follows a **consistent and predictable structure**:

```text
<topic>/
├── README.md        # Concept explanation (why it matters)
├── lab.md           # Hands-on task (exam-style wording)
├── solution.yaml    # Reference solution (after you try)
└── cleanup.yaml     # Optional cleanup
```

### Why this matters

* You can practice **under time pressure**
* You learn **kubectl speed and accuracy**
* You build real **troubleshooting intuition**

No Helm. No abstractions. Just Kubernetes.

---

## ⏱️ CKA-Oriented by Design (Without Being Exam-Only)

While this repo supports the **CKA exam**, it is **not limited to memorization or shortcuts**.

You will learn:

* How Kubernetes *actually works*
* Why certain failures happen
* How to debug under pressure
* How to think like a cluster administrator

Mock exams are included for those who want to **validate exam readiness**.

---

## 🚀 How to Use This Repository

### Recommended learning flow

1. Start with `fundamentals/`
2. Progress through `workloads/` and `scheduling/`
3. Practice `networking/`, `storage/`, and `security/`
4. Spend serious time in `troubleshooting/`
5. Finish with `cka-mock-exams/`

You can also jump directly to any topic if you’re revising.

---

## 📖 Requirements

* A running Kubernetes cluster (local or remote)
* kubectl configured and working
* Curiosity and willingness to experiment

> ⚠️ Cloud providers, minikube, kind, k3s, etc. are intentionally **not prescribed**. Use what you are comfortable with.

---

## 🧠 Guiding Principles

* **Kubernetes first** – everything here maps to Kubernetes concepts
* **Practice over theory**
* **Minimal tooling, maximum clarity**
* **Real-world relevance over toy examples**

---

## 📌 Disclaimer

This project is **not affiliated with, endorsed by, or sponsored by** the CNCF or the Linux Foundation.

CKA® is a registered trademark of the Linux Foundation.

---

## 🤝 Contributing

Contributions are welcome in the form of:

* New labs
* Better troubleshooting scenarios
* Improvements to explanations

Please keep all contributions **Kubernetes-focused** and aligned with the bootcamp philosophy.

---

## ⭐ Final Note

If this repository helps you:

* understand Kubernetes better
* gain confidence
* clear your CKA exam

consider giving it a ⭐ and sharing it with others.

Happy learning and happy debugging 🚀
