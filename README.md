# Kubernetes-Zero-To-Hero

This repository contains the learning roadmap for mastering Kubernetes—from the absolute fundamentals to Kubernetes internals, platform engineering, and production-grade deployments.

---

# Topics Covered

## Kubernetes Foundations

- Kubernetes Fundamentals
- Container Orchestration
- Kubernetes Architecture
- Control Plane Components
- Worker Node Components
- Kubernetes API
- Kubernetes Resources & Objects
- Kubernetes Object Anatomy
- Kubernetes Object Lifecycle
- Desired State Model
- Reconciliation Loop
- Kubernetes Installation
- kubeadm
- Kind
- Minikube
- K3s
- kubectl
- kubeconfig
- Contexts
- Namespaces
- Kubernetes YAML
- Manifest Best Practices

---

## Kubernetes API & Request Lifecycle

- Complete Journey of `kubectl apply`
- kubectl Internals
- Kubernetes REST API
- API Server Request Lifecycle
- Authentication Pipeline
- Authorization Pipeline
- Admission Controllers
- Object Validation
- Object Defaulting
- API Storage Layer
- etcd Write Operations
- Watch API
- Watch Notifications
- Controller Reconciliation
- Deployment Controller
- ReplicaSet Controller
- Scheduler Workflow
- kubelet Workflow
- Container Runtime Workflow

---

## Kubernetes Workloads

- Pods
- Pod Lifecycle
- Init Containers
- Sidecar Containers
- Ephemeral Containers
- Static Pods
- ReplicaSets
- Deployments
- Rolling Updates
- Deployment Strategies
- StatefulSets
- Headless Services
- DaemonSets
- Jobs
- CronJobs
- Horizontal Scaling
- Vertical Scaling
- Pod Disruption Budgets
- Priority Classes
- RuntimeClass

---

## Kubernetes Networking

- Linux Networking Fundamentals
- Network Namespaces
- Virtual Ethernet (veth)
- Linux Bridge
- Routing Tables
- iptables
- conntrack
- Kubernetes Networking Model
- Container Network Interface (CNI)
- CNI Plugins
- Pod-to-Pod Communication
- Pod-to-Service Communication
- Services
- EndpointSlices
- kube-proxy
- CoreDNS
- Ingress
- Gateway API
- Network Policies
- Service Mesh

---

## Kubernetes Storage

- Volumes
- Persistent Volumes (PV)
- Persistent Volume Claims (PVC)
- StorageClasses
- Container Storage Interface (CSI)
- CSI Controller
- CSI Node
- Dynamic Provisioning
- Volume Snapshots
- Volume Expansion
- Ephemeral Volumes
- Storage Performance

---

## Kubernetes Scheduling

- Scheduler Architecture
- Scheduling Queue
- Scheduler Framework
- Filter Plugins
- Score Plugins
- Binding Process
- Node Selectors
- Node Affinity
- Pod Affinity
- Pod Anti-Affinity
- Taints
- Tolerations
- Topology Spread Constraints
- Resource Requests & Limits
- Quality of Service (QoS)
- Pod Evictions

---

## Kubernetes Security

- Authentication
- Authorization
- RBAC
- Service Accounts
- Secrets
- ConfigMaps
- Security Contexts
- Pod Security Admission
- Admission Controllers
- Validating Admission Policy (CEL)
- Mutating Admission Webhooks
- Validating Admission Webhooks
- Network Policies
- Image Security
- Software Supply Chain Security
- Audit Logging
- Secrets Encryption
- Runtime Security

---

## Kubernetes Internals

- API Server Internals
- etcd Internals
- Raft Consensus Algorithm
- MVCC
- Watch Cache
- Controller Manager
- Shared Informers
- Informers
- DeltaFIFO
- WorkQueue
- Reconciliation Loop Internals
- kubelet Internals
- PLEG
- Status Manager
- Volume Manager
- kube-proxy Internals
- containerd Internals
- OCI Runtime
- Container Runtime Interface (CRI)
- Kubernetes API Machinery
- Server Side Apply
- Garbage Collector
- Finalizers
- API Aggregation
- Kubernetes Source Code Walkthrough

---

## Extending Kubernetes

- Custom Resource Definitions (CRDs)
- API Extensions
- Custom Controllers
- controller-runtime
- Kubebuilder
- Operator SDK
- Building Operators
- Dynamic Admission Controllers
- Aggregated APIs
- Building Internal Developer Platforms

---

## Production Kubernetes

- High Availability Clusters
- Multi-Master Architecture
- Backup & Disaster Recovery
- Cluster Upgrades
- Monitoring
- Logging
- Distributed Tracing
- Performance Tuning
- Capacity Planning
- Cluster Autoscaler
- Horizontal Pod Autoscaler (HPA)
- Vertical Pod Autoscaler (VPA)
- GitOps
- Multi-Cluster Architecture
- Production Troubleshooting
- Kubernetes Design Patterns
- Real-World Production Architectures

---

## By the End of This Masterclass, You Will Understand

- Kubernetes architecture from first principles
- How Kubernetes processes every API request internally
- How workloads are scheduled and managed
- How Kubernetes networking works under the hood
- How persistent storage is provisioned and managed
- How Kubernetes secures workloads and clusters
- How the control plane functions internally
- How to extend Kubernetes using CRDs, controllers, and operators
- How to design, operate, and troubleshoot production-grade Kubernetes clusters
- Kubernetes internals beyond what is covered in certification courses
