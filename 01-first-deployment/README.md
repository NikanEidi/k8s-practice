# 01: First Deployment

## Goal

Run two copies of an nginx web server as a Deployment, then confirm that Kubernetes replaces a Pod automatically when one is deleted.

## What this shows

- A **Deployment** keeps a desired number of Pods running (`replicas: 2`).
- If a Pod is deleted, the Deployment's controller creates a replacement to restore the desired state.
- Pods get their own names, which are generated from the Deployment name.

## Files

- [`deployment.yaml`](deployment.yaml): a Deployment with 2 replicas of `nginx:1.27`, exposing port 80.

## Steps

```bash
# 1. Start a local cluster (Docker Desktop must be running)
kind create cluster

# 2. Confirm the node is ready
kubectl get nodes

# 3. Create the Deployment
kubectl apply -f deployment.yaml

# 4. List the Pods (expect 2, status Running)
kubectl get pods

# 5. Delete one Pod and watch it being replaced
kubectl delete pod <pod-name>
kubectl get pods
```

## Expected result

- After step 4: two Pods named `hello-nginx-<hash>-<id>`, both `Running`.
- After step 5: the deleted Pod is gone and a new Pod with a different name appears, so the count returns to 2.

## Clean up

```bash
kubectl delete -f deployment.yaml
kind delete cluster
```

## Observations

_To be filled in after running the exercise._
