# ArgoCD ApplicationSet Repository
This repository contains configurations for ArgoCD, including ApplicationSet and Helm-based deployments for various environments. Below is a description of the different YAML files and directories available in this repository.

## `argocd/appset.yaml`
This file defines an `ApplicationSet` to manage multiple ArgoCD applications dynamically. It uses a list generator to deploy the following environments:

* **my-dev:** for development namespace and resources.
* **my-prod:** for production namespace and resources.
* **my-stage:** for staging environment.
* **my-monitoring:** for monitoring environment.

Each application pulls from the specified Git repository and automatically syncs with ArgoCD.

### Key Features:
* Auto-creates namespaces for each environment (`CreateNamespace=true`).
* Enables self-healing and pruning for all applications.
* Supports multiple Git repositories for different environments.

## `argocd/my-helm.yaml`
This file defines an ArgoCD application for deploying the httpbin service using Helm charts.

### Key Features:
* Uses Helm to deploy the `httpbin` chart.
* Pulls from the repository: `https://matheusfm.dev/charts.`
* Automatically syncs and applies changes with self-healing and pruning enabled.
* Configured to deploy the service as a NodePort type.

## `argocd/my-nginx.yaml`
This ArgoCD application is responsible for deploying an Nginx service via Helm.

### Key Features:
* Uses Helm to deploy the `my-nginx` chart.
* Pulls the chart from a GitHub repository.
* Target revision set to `main` with namespace `dev`.
* Configured with `NodePort` service type.
* Automated synchronization with self-healing and pruning enabled.


## `argocd/sync.yaml`
The `sync.yaml` file defines a simple ArgoCD application for syncing configurations from this repository's argocd directory.

### Key Features:
* Syncs with the `argocd` namespace.
* Automatically applies changes with self-healing and pruning enabled.

## Environments
`dev/`
* Contains Kubernetes manifests for deploying services in the `dev` environment.
  - `deploy.yaml`: Deployment resource for the dev environment.
  - `svc.yaml`: Service resource for the dev environment.

`stage/`
* Contains Kubernetes manifests for deploying services in the `stage` environment.
  - `deploy.yaml`: Deployment resource for the stage environment.
  - `svc.yaml`: Service resource for the stage environment.

`my-nginx/`
* Helm chart directory for `my-nginx`.
  - `.helmignore`: Files to be ignored by Helm.
  - `Chart.yaml`: Metadata for the Helm chart.
  - `values.yaml`: Default values for the chart.
  - `templates/`: Directory containing Helm templates for the application.

## Sync and Automation
All applications defined in this repository are configured to automatically sync with ArgoCD. The `syncPolicy` is enabled for each application, allowing ArgoCD to self-heal and prune resources as needed.
