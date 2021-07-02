# Chart values for Traefik

ENSURE THAT YOU HAVE SOME SORT OF VOLUME MANAGER INSTALLED (LIKE LONGHORN)

Helm is of course required
A configured kubectl is also of course required

## Installing and Upgrading Traefik

install:

```bash
helm install traefik traefik/traefik --namespace=kube-system --values=traefik-chart-values.yaml
```

upgrade:

```bash
helm upgrade traefik traefik/traefik --namespace=kube-system --values=traefik-chart-values.yaml
```
