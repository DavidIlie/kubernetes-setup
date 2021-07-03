# Kubernetes Setup

This is my documentation for installing a HA k3s cluster in my homelab, but it can be easily modified for yours.

If you follow this guide entirely, you should be awarded with

-   A highly available Kubernetes cluster
-   etcd for master nodes
-   has rancher installed
-   has traefik 2 installed
-   has authelia installed (for protecting traefik routes)
-   nfs persistent volumes support (from NFS servers like from TrueNAS and so on)

if you want all these setup make sure you run them in this order:

first of all: MAKE SURE ALL NODES ARE UBUNTU 20.04 (or any lts version of Ubuntu)

-   1 - keepalived | files to put in /etc/keepalived
-   2 - ansible-setup | contains install and uninstall ansible playbooks (make sure to change all the ips)
-   3 - cert-manager | file to install cert-manager
-   4 - metalllb | files to setup metalllb (order: namespace.yaml, metallb.yaml, config.yaml)
-   5 - rancher | follow readme in there
-   6 - traefik | helm charts to install traefik
-   7 - nfs pvc | make a persistent volume with nfs shares
-   8 - authelia | protect your routes with username/password

## Commons

When creating a new ingress, make sure to add this annotation:
`kubernetes.io/ingress.class=traefik-external`

When creating a protected ingress route, make sure to add this annotation:
`traefik.ingress.kubernetes.io/router.middlewares=default-authelia@kubernetescrd`
