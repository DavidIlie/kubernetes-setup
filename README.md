# Kubernetes Setup

This is my documentation for installing a HA k3s cluster in my homelab, but it can be easily modified for yours.

MAKE SURE THAT ALL NODES ARE USING UBUNTU 20.04!!!

if you want all these setup make sure you run them in this order:

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
