Kubernetes Lectures

Lecture 01 

Section 1 — Introduction
Imagine you're building an application like Netflix or Spotify.
Initially, everything works perfectly.
You have:
One application
One Docker container
One server
That’s Simple.

+-------------------------+
| Server                  |
|                         |
|  Docker Container       |
|  Your Application       |
|                         |
+-------------------------+

But your application becomes popular.
Now you need:
Multiple servers
Hundreds of containers
Continuous deployments
High availability
Automatic recovery
Scaling
Suddenly everything becomes difficult.
This is exactly why Kubernetes exists.

Section 2 — What is Kubernetes?
Official Definition
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications.
That sounds complicated.
Let's simplify it.
Imagine Docker is like shipping containers.
Docker knows how to create and run containers.
But Docker does NOT know:
Which server should run a container?
What happens if the server dies?
How many copies should exist?
How to expose applications?
How to update without downtime?
How to scale automatically?
Kubernetes answers all these questions.
Think of Docker as a car.
Kubernetes is the entire traffic management system controlling thousands of cars.

Simple Definition
Kubernetes is a platform that continuously ensures your applications are running exactly the way you want them to run.
Notice the word continuously.
That word is the heart of Kubernetes.

Section 3 — Why was Kubernetes Created?
Before Kubernetes, companies managed applications manually.
Example:
Suppose you have:

App A

Running on Server 1

Traffic increases.
You manually create another server.

Server 1
App A

Server 2
App A

Traffic increases again.
Create another server.
Now imagine this happening hundreds of times.
Every deployment becomes stressful.
Now imagine a server crashes at 3 AM.
Someone gets paged.
They SSH into the machine.
Restart the application.
This doesn't scale.
Google faced this problem over a decade ago.
Google was running billions of containers.
Humans couldn't manage them manually.
So Google built an internal orchestration system called Borg.
Years later, many of Borg's ideas were released as Kubernetes.

Section 4 — What Problems Does Kubernetes Solve?
Let's understand the real-world problems.

Problem 1 — Manual Deployment
Without Kubernetes:

Developer

↓

Docker Build

↓

Copy Image

↓

SSH

↓

Run Docker

↓

Hope Everything Works

Every deployment involves manual effort.
With Kubernetes:

Developer

↓

Push Code

↓

CI/CD

↓

Kubernetes

↓

Deployment Happens Automatically


Problem 2 — Server Failure
Imagine this:

Server 1

Container Running

Server crashes.

Server 1

Dead

Application is gone.
Customers cannot access it.
Without Kubernetes:
Someone notices.
Someone fixes it.
With Kubernetes:

Desired:

3 Containers

Current:

2 Containers

↓

Kubernetes Creates New One

↓

Back to 3

No human intervention.

Problem 3 — Scaling
Morning traffic:

2 Containers

Evening traffic:

20 Containers

Night:

2 Containers

Without Kubernetes:
Humans manually create containers.
With Kubernetes:
Auto Scaling.
Kubernetes creates containers automatically.
Removes them automatically.

Problem 4 — Zero Downtime Updates
Suppose version 1 is running.

Users

↓

Version 1

You release Version 2.
Without Kubernetes:
Stop Version 1.
Start Version 2.
Downtime.
With Kubernetes:

Version 1
Version 2

↓

Traffic shifts slowly

↓

Version 1 Removed

Users never notice.

Problem 5 — Self Healing
Container crashes.
Without Kubernetes:

Application Down

With Kubernetes:

Container Crashes

↓

Kubernetes Detects Failure

↓

Starts New Container

↓

Application Healthy Again


Problem 6 — Resource Utilization
Suppose one server has:

16 CPUs
64 GB RAM

Application only needs:

2 CPUs
4 GB RAM

Most resources remain unused.
Kubernetes intelligently schedules workloads to maximize resource utilization across servers.

Section 5 — Why Container Orchestration is Needed
Docker runs containers.
But imagine managing 5,000 containers.
Questions arise:
Which server should run a container?
Which server has enough memory?
Which server has enough CPU?
How should traffic reach containers?
What if a node dies?
What if a container dies?
How do updates happen?
How do rollbacks happen?
How do we scale?
Humans cannot answer these continuously.
An orchestrator can.
That's Kubernetes.

What does "Orchestration" Mean?
Think of an orchestra.
There are:
Piano
Guitar
Violin
Drums
Everyone plays independently.
Without a conductor:
Chaos.
The conductor coordinates everyone.
Kubernetes is the conductor.
Containers are musicians.
Nodes are the stage.
Applications become synchronized.

Section 6 — Kubernetes Ecosystem
Kubernetes itself is only one part of a much larger cloud-native ecosystem. While Kubernetes provides orchestration, it relies on or integrates with many other tools to build production-grade platforms.

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

Key ecosystem components
Container Runtime – Runs containers (e.g., containerd, CRI-O).
Container Registry – Stores container images.
CNI (Container Network Interface) – Provides pod networking.
CSI (Container Storage Interface) – Connects Kubernetes to storage systems.
Ingress Controller – Routes external HTTP/HTTPS traffic into the cluster.
Monitoring – Prometheus collects metrics; Grafana visualizes them.
Logging – Fluent Bit, Loki, Elasticsearch, and Kibana help collect and analyze logs.
Service Mesh – Istio or Linkerd add advanced traffic management, observability, and security.
GitOps – Tools like Argo CD and Flux continuously synchronize the cluster with the desired configuration stored in Git.
The important takeaway is that Kubernetes is the central platform that coordinates all of these components, but it is not intended to replace them.

Section 7 — The Heart of Kubernetes: The Reconciliation Loop
If you understand only one concept from this video, let it be this one.
Kubernetes is declarative, not imperative.
Imperative approach
You tell the system exactly what to do:

Run this container.

Restart it.

Scale it.

Delete it.

Every action is manual.
Declarative approach
Instead, you describe the desired end state:

I want:

3 replicas

Image: nginx:1.27

Port: 80

Always running

You do not specify how to achieve that state.
Kubernetes continuously works to make reality match your declaration.
This continuous process is called the Reconciliation Loop.
Example
Desired state:

Replicas = 3

Current state:

Replicas = 2

The control plane notices the difference:

Desired: 3
Current: 2
Difference: 1

It schedules another Pod.
Now:

Desired: 3
Current: 3

The cluster is back in the desired state.
Another example
You accidentally delete a Pod.

Pod Deleted

↓

Current = 2

↓

Desired = 3

↓

Controller notices mismatch

↓

Scheduler selects a node

↓

Kubelet starts a new Pod

↓

Current = 3

No administrator has to intervene.
The control loop

User defines Desired State
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
Take corrective   Continue
    action        watching
        │
        ▼
Current state updated
        │
        └──────────────► Repeat forever

This loop runs continuously for deployments, replicas, services, nodes, storage, networking, and many other Kubernetes resources. It is the fundamental mechanism that gives Kubernetes its self-healing, scaling, and automation capabilities.
