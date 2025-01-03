# Initial deployment
< These are temporary steps that still need automation
{is.warning}

After running terraform to deploy the Talos cluster, complete the steps below to setup the kubernetes apps.
  1. Get the initial Argocd password.
    1. `k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`
    1. Paste the password into the browser `http://10.10.10.86:80`.
    1. Run the deployment command `k kustomize --enable-helm --load-restrictor=LoadRestrictionsNone /mnt/ark/build/k8s-apps/argocd-build | k apply -f-`
