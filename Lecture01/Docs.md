# Kubernetes Lecture 01 — Introduction to Kubernetes

---

# Section 1 — Introduction

Imagine you're building an application like **Netflix** or **Spotify**.

Initially, everything works perfectly.

You have:

- One application
- One Docker container
- One server

That's simple.

```text
+-------------------------+
| Server                  |
|                         |
|  Docker Container       |
|  Your Application       |
|                         |
+-------------------------+
```

But as your application becomes popular, things change.

Now you need:

- Multiple servers
- Hundreds of containers
- Continuous deployments
- High availability
- Automatic recovery
- Scaling

Suddenly, managing everything manually becomes extremely difficult.

This is exactly why **Kubernetes** exists.

---

# Section 2 — What is Kubernetes?

## Official Definition

> Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications.

That sounds complicated.

Let's simplify it.

Imagine Docker as shipping containers.

Docker knows how to:

- Create containers
- Start containers
- Stop containers

But Docker **does not know**:

- Which server should run a container?
- What happens if the server dies?
- How many copies of the application should exist?
- How should applications be exposed?
- How should updates happen without downtime?
- How should applications scale automatically?

Kubernetes answers all of these questions.

Think of it like this:

- **Docker = Car**
- **Kubernetes = Entire traffic management system controlling thousands of cars**

---

## Simple Definition

> Kubernetes is a platform that continuously ensures your applications are running exactly the way you want them to run.

The most important word here is:

**Continuously**

That single word represents the heart of Kubernetes.

---

# Section 3 — Why was Kubernetes Created?

Before Kubernetes, applications were managed manually.

Imagine an application running on one server.

```text
Server 1
└── App A
```

Traffic increases.

You manually provision another server.

```text
Server 1
└── App A

Server 2
└── App A
```

Traffic increases again.

Provision another server.

Now imagine doing this hundreds or even thousands of times.

Every deployment becomes stressful.

Now imagine a server crashes at **3 AM**.

Someone gets paged.

They:

- SSH into the server
- Restart the application
- Verify everything is working

This approach doesn't scale.

Google faced this exact problem over a decade ago.

They were running **billions of containers**.

Managing them manually became impossible.

Google built an internal orchestration platform called **Borg**.

Years later, many of Borg's core ideas became **Kubernetes**.

---

# Section 4 — What Problems Does Kubernetes Solve?

## Problem 1 — Manual Deployment

Without Kubernetes

```text
Developer
    │
Docker Build
    │
Copy Image
    │
SSH into Server
    │
Run Docker
    │
Hope Everything Works
```

Every deployment requires manual effort.

With Kubernetes

```text
Developer
    │
Push Code
    │
CI/CD Pipeline
    │
Kubernetes
    │
Deployment Happens Automatically
```

---

## Problem 2 — Server Failure

Imagine this scenario.

```text
Server 1
└── Container Running
```

The server crashes.

```text
Server 1
└── Dead
```

The application disappears.

Customers cannot access it.

### Without Kubernetes

Someone notices the outage.

Someone manually fixes it.

### With Kubernetes

Desired State

```text
3 Containers
```

Current State

```text
2 Containers
```

Kubernetes detects the difference.

```text
Desired = 3
Current = 2
```

It automatically creates another container.

```text
Current = 3
```

No human intervention is required.

---

## Problem 3 — Scaling

Morning traffic

```text
2 Containers
```

Evening traffic

```text
20 Containers
```

Night traffic

```text
2 Containers
```

Without Kubernetes

Humans manually create and remove containers.

With Kubernetes

Auto Scaling automatically:

- Creates containers
- Removes containers

Based on demand.

---

## Problem 4 — Zero Downtime Updates

Version 1 is currently serving users.

```text
Users
   │
Version 1
```

You release Version 2.

### Without Kubernetes

```text
Stop Version 1

↓

Start Version 2

↓

Downtime
```

### With Kubernetes

```text
Version 1
Version 2

↓

Traffic gradually shifts

↓

Version 1 removed
```

Users never notice the deployment.

---

## Problem 5 — Self-Healing

Container crashes.

Without Kubernetes

```text
Application Down
```

With Kubernetes

```text
Container Crashes

↓

Failure Detected

↓

New Container Started

↓

Application Healthy Again
```

---

## Problem 6 — Resource Utilization

Suppose a server has:

- 16 CPUs
- 64 GB RAM

Your application only needs:

- 2 CPUs
- 4 GB RAM

Most resources remain unused.

Kubernetes intelligently schedules workloads across servers to maximize resource utilization.

---

# Section 5 — Why Container Orchestration is Needed

Docker runs containers.

But imagine managing **5,000 containers**.

Questions immediately arise.

- Which server should run a container?
- Which server has enough CPU?
- Which server has enough memory?
- How should traffic reach containers?
- What happens if a node dies?
- What happens if a container crashes?
- How do updates happen?
- How do rollbacks happen?
- How do applications scale?

Humans cannot answer these questions continuously.

An orchestrator can.

That orchestrator is Kubernetes.

---

## What Does "Orchestration" Mean?

Think of an orchestra.

There are many musicians.

- Piano
- Guitar
- Violin
- Drums

Each musician knows how to play.

Without a conductor...

Chaos.

The conductor coordinates everyone.

In Kubernetes:

- **Kubernetes = Conductor**
- **Containers = Musicians**
- **Nodes = Stage**

The result is a synchronized application platform.

---

# Section 6 — Kubernetes Ecosystem

Kubernetes is only one part of the cloud-native ecosystem.

It provides orchestration, but integrates with many surrounding technologies.

```text
                 Developers
                      │
                      ▼
               Source Code (Git)
                      │
                      ▼
                 CI/CD Pipeline
        (GitHub Actions, Jenkins, GitLab)
                      │
                      ▼
               Container Image
          (Docker, Buildah, Kaniko)
                      │
                      ▼
             Container Registry
     (Docker Hub, ECR, ACR, GCR, Harbor)
                      │
                      ▼
                 Kubernetes
                      │
      ┌───────────────┼────────────────┐
      ▼               ▼                ▼
 Networking      Storage          Scheduling
(CNI Plugins)   (CSI Drivers)     (Scheduler)
      │               │                │
      └───────────────┼────────────────┘
                      ▼
                 Running Pods
                      │
      ┌───────────────┼────────────────┐
      ▼               ▼                ▼
 Monitoring      Logging         Security
(Prometheus)      (EFK/Loki)     (RBAC, OPA)
      │               │                │
      ▼               ▼                ▼
 Visualization    Dashboards      Policy
   (Grafana)
```

---

## Key Ecosystem Components

### Container Runtime

Runs containers.

Examples:

- containerd
- CRI-O

---

### Container Registry

Stores container images.

Examples:

- Docker Hub
- Amazon ECR
- Azure ACR
- Google GCR
- Harbor

---

### CNI (Container Network Interface)

Provides networking for Pods.

---

### CSI (Container Storage Interface)

Connects Kubernetes to external storage systems.

---

### Ingress Controller

Routes external HTTP and HTTPS traffic into the cluster.

---

### Monitoring

- Prometheus
- Grafana

---

### Logging

- Fluent Bit
- Loki
- Elasticsearch
- Kibana

---

### Service Mesh

Examples:

- Istio
- Linkerd

Provides:

- Traffic management
- Observability
- Security

---

### GitOps

Examples:

- Argo CD
- Flux

Continuously synchronizes the Kubernetes cluster with the desired configuration stored in Git.

---

## Key Takeaway

Kubernetes is the central orchestration platform that coordinates all these components.

It integrates with them rather than replacing them.

---

# Section 7 — The Heart of Kubernetes: The Reconciliation Loop

If you understand only one concept from this lecture, let it be this one.

Kubernetes is **declarative**, not imperative.

---

## Imperative Approach

You tell the system exactly what to do.

Examples:

- Run this container.
- Restart it.
- Scale it.
- Delete it.

Every action is manually executed.

---

## Declarative Approach

Instead of specifying the steps, you describe the desired end state.

Example

```yaml
Replicas: 3
Image: nginx:1.27
Port: 80
Always Running
```

You never explain **how** to achieve this.

Kubernetes continuously works to make reality match your declaration.

This continuous process is called the **Reconciliation Loop**.

---

## Example 1

Desired State

```text
Replicas = 3
```

Current State

```text
Replicas = 2
```

The control plane detects the difference.

```text
Desired = 3

Current = 2

Difference = 1
```

Kubernetes schedules another Pod.

```text
Desired = 3

Current = 3
```

The cluster is back in the desired state.

---

## Example 2

A Pod is accidentally deleted.

```text
Pod Deleted

↓

Current = 2

↓

Desired = 3

↓

Controller Detects Mismatch

↓

Scheduler Selects Node

↓

Kubelet Starts New Pod

↓

Current = 3
```

No administrator intervention is required.

---

## The Reconciliation Loop

```text
User Defines Desired State
            │
            ▼
      Kubernetes API Server
            │
            ▼
       Controllers Watch
            │
            ▼
Compare Desired vs Current State
            │
     Are they different?
        ┌──────┴──────┐
       Yes           No
        │             │
        ▼             ▼
Take Corrective   Continue
    Action        Watching
        │
        ▼
Current State Updated
        │
        └──────────────► Repeat Forever
```

This loop continuously runs for:

- Deployments
- ReplicaSets
- Pods
- Services
- Nodes
- Storage
- Networking
- Jobs
- StatefulSets
- DaemonSets

This reconciliation process is the fundamental mechanism behind Kubernetes' automation, self-healing, scaling, and resilience.

---

# Key Takeaways

By the end of this lecture, you should understand:

- Why Kubernetes was created
- What Kubernetes is
- The problems Kubernetes solves
- Why container orchestration is necessary
- The Kubernetes ecosystem
- The concept of declarative infrastructure
- The importance of the Reconciliation Loop

These concepts form the foundation for everything else in Kubernetes.