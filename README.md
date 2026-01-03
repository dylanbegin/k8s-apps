> [!NOTE]
> This is a mirrored repo.

> [!WARNING]
> This README is still under development!

# 󱃾 Kubernetes Cluster Repo
> [!IMPORTANT]
> This repo is built for my own environment so please review all configurations to verify compatibility!

> [!TIP]
> This repo is part of my IaC automation series. If you are building this in mind please follow my repo's in the order below.

1.  [terraform-iso-get](https://github.com/dylanbegin/terraform-iso-get)
1.  [packer](https://github.com/dylanbegin/packer)
1.  [terraform-core](https://github.com/dylanbegin/terraform-core)
1.  [ansible](https://github.com/dylanbegin/ansible)
1.  [terraform-talos](https://github.com/dylanbegin/terraform-talos)
1.  *you are here* [k8s-apps](https://github.com/dylanbegin/k8s-apps)

# Initial deployment
> [!NOTE]
> These are temporary steps that still need automation.

After running terraform to deploy the Talos cluster, complete the steps below to setup the kubernetes apps.
  1. Before we build out the apps we need to stage the database and configure all databases.
    1. `kubectl kustomize --enable-helm --load-restrictor=LoadRestrictionsNone /path-to/k8s-apps/databases | kubectl apply -f-`
    1. Build databases:
      1. `create user <username> with password '<password>';`
      1. `create database <database> with owner <username>;`
      1. `grant all privileges on database <database> to <username>;`
      1. `grant connect on database <database> to <username>;`
      1. The current list of databases needs to be created: `authentik` `freshrss` `gitea` `hassos` `nextcloud` `vaultwarden` `wikijs`
  1. Get the initial Argocd password.
    1. `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`
    1. Save this password into your password manager.
  1. Run the deployment command `kubectl kustomize --enable-helm --load-restrictor=LoadRestrictionsNone /path-to/k8s-apps/argocd-build | kubectl apply -f-`
