# Kubernetes Setup

This is my documentation for installing a HA k3s cluster in my homelab, but it can be easily modified for yours.

If you follow this guide entirely, you should be awarded with

-   A highly available Kubernetes cluster
-   etcd for master nodes
-   has rancher installed
-   has traefik 2 installed
-   has authelia installed (for protecting traefik routes)
-   nfs persistent volumes support (from NFS servers like from TrueNAS and so on)

If you want to get this setup for your own homelab, the folders are organised in their exact order by numbers so make sure to follow them. Also, make sure nodes are not running Ubuntu 21.04 as there are some errors with installing Rancher in that version.

This has been my research for the past year since I've been messing around with Kubernetes since July 2020. Hope this helps somebody!

## Commons

When creating a new ingress, make sure to add this annotation:
`kubernetes.io/ingress.class=traefik-external`

When creating a protected ingress route, make sure to add this annotation:
`traefik.ingress.kubernetes.io/router.middlewares=default-authelia@kubernetescrd`
