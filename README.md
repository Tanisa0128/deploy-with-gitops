#  GitOps Deployment with Flux

This repository contains the **GitOps configuration** for deploying applications into a Kubernetes cluster using [Flux](https://fluxcd.io/).  
It works together with the [manage-gitops-pipeline](https://github.com/Tanisa0128/manage-gitops-pipeline) repo, which builds Docker images and pushes them for deployment.

---

##  What’s Inside?

### 1. HelmRelease (`podinfo.yaml`)
- Deploys the [Podinfo](https://github.com/stefanprodan/podinfo) app.  
- Custom settings:
  - UI color and greeting message  
  - Service type: **NodePort** (port `32570`)  

### 2. Namespace (`namespace.yaml`)
- Creates and manages the **podinfo** namespace.

### 3. Helm Repository (`podinfo-source-helm-repo.yaml`)
- Defines the external Helm repository where the **podinfo** chart comes from.

### 4. Kustomization (`kustomization.yaml`)
- Groups related resources together.  
- Helps Flux know what to apply and manage in the cluster.

### 5. Flux System (`gotk-components.yaml`, `gotk-sync.yaml`)
- Installed by Flux bootstrap.  
- Ensures GitOps workflow and keeps cluster in sync with this repo.

### 6. Cluster Folder (`clusters/podinfo-cluster/`)
- Contains all files for this environment (can be extended for more clusters later).

---

##  How It Works

1. **Flux Components (`flux-system/`)**
   - Manages reconciliation between Git and the cluster.
   - Ensures Kubernetes state matches this repository.

2. **Podinfo App (`podinfo/`)**
   - Deploys the [podinfo](https://github.com/stefanprodan/podinfo) application using HelmRelease.
   - Custom values are applied:
     - UI color → `#cd5b1c`
     - Greeting message → `"Hello, I am podinfo version latest-20250621130825. Hi Tanisa, Good evening."`
     - Service type → `NodePort` (on port `32570`)

3. **Sources (`sources/helm-repository/`)**
   - Declares the Helm repository where the podinfo chart is pulled from.

---

##  Benefits
- Automated deployments  
- Version-controlled manifests  
- Easy rollback via Git  
- Clear separation of concerns  

---

---

## 📝 Notes
- You can add more apps by creating new HelmReleases.  
- Extend this repo to manage multiple clusters under `clusters/`.  
- All changes are **Git-driven** → Flux ensures the cluster matches this repo.  

