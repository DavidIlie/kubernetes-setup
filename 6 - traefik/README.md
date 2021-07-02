# Chart values for Traefik

make sure you fill in the correct information in both `traefik-chart-values.yaml` and in `traefik-config.yaml` to prevent errors

ENSURE THAT YOU HAVE SOME SORT OF VOLUME MANAGER INSTALLED (LIKE LONGHORN)

## Installing and Upgrading Traefik

install:

```bash
helm install traefik traefik/traefik --namespace=kube-system --values=traefik-chart-values.yaml
```

upgrade:

```bash
helm upgrade traefik traefik/traefik --namespace=kube-system --values=traefik-chart-values.yaml
```
