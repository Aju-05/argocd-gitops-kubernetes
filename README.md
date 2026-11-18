# Kubernetes GitOps with Argo CD

This repository keeps Kubernetes application configuration in Git and uses Argo CD to reconcile a cluster with the desired state.

## Layout
- `apps/sample-service/base`: reusable Deployment and Service
- `apps/sample-service/overlays/dev`: development replica and image settings
- `argocd/application.yaml`: Argo CD Application definition

## Prerequisites
A Kubernetes cluster and Argo CD installation are required. Install Argo CD using the official documentation for your cluster, then apply the Application manifest after updating the repository URL and target namespace.

## Bootstrap
```bash
kubectl create namespace argocd
# Install Argo CD using the official installation procedure.
kubectl apply -f argocd/application.yaml
```

Update the placeholder Git URL in `argocd/application.yaml` to this repository's HTTPS or SSH URL before applying it.

## Reconciliation and rollback
Argo CD continuously compares the live cluster state with Git. Revert a manifest change in Git to request a rollback through reconciliation. For incident response, inspect Argo CD application health and Kubernetes events before changing live resources manually.

## Security considerations
Use a dedicated repository deploy key or GitHub App, restrict Argo CD project destinations, use RBAC, and store secrets in an approved secret manager integration. The sample intentionally contains no credentials or Kubernetes Secret values.

## Status
Manifests are examples for review. No cluster sync or live deployment is claimed.
