# k8s-practice

Hands-on Kubernetes exercises, from a first Deployment to Services, scaling, and health checks. Each exercise is small, runs on a local cluster, and includes the manifests and the commands used to verify it.

## Goals

- Understand the core Kubernetes objects (Pod, Deployment, Service) and how they relate.
- Operate a cluster with `kubectl` using the same commands that work on managed clusters (EKS, AKS, GKE) and OpenShift.
- Keep a short, honest record of what was run and what was observed.

## Prerequisites

- macOS (or Linux/Windows with equivalent tools)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/), running while practicing
- [Homebrew](https://brew.sh)
- `kind` and `kubectl`:

```bash
brew install kind kubectl
```

## Core concepts

| Term | Meaning |
|---|---|
| **Node** | A machine (VM or physical) that runs workloads. |
| **Pod** | The smallest deployable unit. Usually one container. |
| **Container** | The packaged application, typically built with Docker. |
| **Deployment** | Declares a desired number of identical Pods and keeps that count running. |
| **Service** | A stable network address that load-balances traffic across matching Pods. |
| **kubectl** | The command-line client that talks to the cluster API. |
| **kind** | Runs a local Kubernetes cluster inside Docker. For learning, not production. |

**Key point:** Kubernetes orchestrates containers but does not build or run them itself. It delegates execution to a container runtime (containerd). Docker is one way to build the images; Kubernetes does not require Docker to be installed on the nodes.

## Exercises

| # | Exercise | Status |
|---|---|---|
| 01 | [First Deployment](01-first-deployment/) | Manifest written, not yet run |

## Repository layout

```
k8s-practice/
├── README.md
├── 01-first-deployment/
│   ├── README.md
│   └── deployment.yaml
└── ...
```

## Notes on managed clusters

`kind` creates the cluster locally. On cloud platforms, the cluster is created with a different tool (`eksctl`, `az aks`, `gcloud container clusters`), but the workload commands (`kubectl apply`, `get`, `describe`, `logs`, `delete`) are identical.
