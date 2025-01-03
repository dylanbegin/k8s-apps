> [!WARNING]
> This README is still under development!

# ![logo](https://icon.horse/icon/kubernetes.io) Kubernetes Cluster Repo
> [!IMPORTANT]
> This repo is built for my own environment so please review all configurations to verify compatibility!

# Initial deployment
> [!NOTE]
> These are temporary steps that still need automation.

After running terraform to deploy the Talos cluster, complete the steps below to setup the kubernetes apps.
  1. Get the initial Argocd password.
    1. `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`
    1. Save this password into your password manager.
  1. Run the deployment command `kubectl kustomize --enable-helm --load-restrictor=LoadRestrictionsNone /path-to/k8s-apps/argocd-build | kubectl apply -f-`
