# install rancher

first create the namespace

```bash
kubectl create namespace cattle-system
```

# helm

make sure helm is installed by doing this below:

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

afterwards add the rancher stable repo

```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
```

then do this to actually download it

```bash
helm repo update
```

afterwards you can install rancher with this command below

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.davidapps.dev \
  --version 2.5.8
```

ensure to change the version when rancher updates

# port forwarding

once rancher is installed do this command to portforward with metallb

```bash
kubectl expose deployment rancher -n cattle-system --type=LoadBalancer --name=rancher-lb --port=443
```