# k8s-practice

Hands-on Kubernetes exercises, run on a local cluster. Each exercise is small and self-contained, and includes the manifests, the commands used, the observed output, and what it shows.

The path runs from a first Deployment to Services, scaling, and health checks.

## Goals

- Understand the core objects (Pod, ReplicaSet, Deployment, Service) and how they relate.
- Use `kubectl` in a way that carries over to managed clusters (EKS, AKS, GKE) and OpenShift.
- Keep an honest record: what was run, what happened, and what was not verified.

## Prerequisites

| Tool | Purpose | Install |
|---|---|---|
| Docker Desktop | Runs the containers that make up the local cluster | [docker.com](https://www.docker.com/products/docker-desktop/) |
| kind | Creates a local Kubernetes cluster inside Docker | `brew install kind` |
| kubectl | Command-line client for the Kubernetes API | `brew install kubectl` |

Docker Desktop must be running whenever you use `kind`.

## Quick start

```bash
kind create cluster          # create a local single-node cluster
kubectl get nodes            # confirm the node is Ready
kind delete cluster          # tear it down when finished
```

## Core concepts

| Term | Meaning |
|---|---|
| **Cluster** | A set of Nodes managed together as one Kubernetes system. |
| **Node** | A machine (VM or physical) that runs Pods. The control plane also runs on a Node. |
| **Pod** | The smallest deployable unit. Runs on a Node and usually holds one container. |
| **Container** | The packaged application, typically built with Docker. |
| **ReplicaSet** | Keeps a fixed number of identical Pods running. Created by a Deployment. |
| **Deployment** | Declares the desired Pods and their template; manages ReplicaSets and rollouts. |
| **Service** | A stable address that load-balances traffic across matching Pods. |
| **kubectl** | The client that sends requests to the cluster's API server. |
| **kind** | Runs a cluster whose Nodes are Docker containers. For learning, not production. |

**Key point:** Kubernetes decides where and how many containers run, and restores them when they fail. It does not build or execute them itself. Execution is handled by a container runtime such as containerd. Docker is a common tool for building images, but Kubernetes does not require Docker on its Nodes.

## Exercises

| # | Exercise | Status | What it covers |
|---|---|---|---|
| 01 | [First Deployment](01-first-deployment/) | Completed | Deployment, replicas, labels and selectors, self-healing |
| 02 | [Service](02-service/) | Completed | Stable addressing, selectors, NodePort vs ClusterIP vs LoadBalancer |
| 03 | [Scaling and rolling updates](03-scaling-and-updates/) | Completed | `kubectl scale`, rolling updates, rollout status/history, rollback |
| 04 | [Health checks](04-health-checks/) | Completed | Readiness vs. liveness probes, httpGet, failureThreshold |
| 05 | [ConfigMap and Secret](05-configmap-and-secret/) | Completed | `envFrom`, why Secrets are encoded not encrypted |
| 06 | [Resource limits and requests](06-resource-limits/) | Completed | Requests vs. limits, CPU throttling vs. OOMKilled |
| 07 | [Namespaces](07-namespaces/) | Completed | Isolation, cluster-scoped vs. namespaced objects, ResourceQuota |

## Repository layout

```
k8s-practice/
├── README.md                     # this file
├── 01-first-deployment/
│   ├── README.md                 # lesson notes, steps, observed results
│   ├── deployment.yaml           # Deployment: hello-nginx (2 replicas)
│   └── deployment-nikan.yaml     # second Deployment, separate label
└── .gitignore
```

## Managed clusters

`kind` creates the cluster locally. On cloud platforms, the cluster itself is created with a different tool (`eksctl`, `az aks`, `gcloud container clusters`). The workload commands (`kubectl apply`, `get`, `describe`, `logs`, `delete`) are the same everywhere.
