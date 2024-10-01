# ArgoCD ApplicationSet Repository
This repository contains configurations for ArgoCD, including ApplicationSet and Helm-based deployments for various environments. Below is a description of the different YAML files and directories available in this repository.

### `argocd/appset.yaml`
This file defines an 'ApplicationSet' to manage multiple ArgoCD applications dynamically. It uses a list generator to deploy the following environments:

my-dev: for development namespace and resources.
my-prod: for production namespace and resources.
my-stage: for staging environment.
my-monitoring: for monitoring environment.
