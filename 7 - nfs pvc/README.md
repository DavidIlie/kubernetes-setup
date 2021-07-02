# NFS Persistent Volumes

You first need to create a NFS share but make sure you give it the right permissions with the command below:

(if your nas is using Truenas or Freenas, you can enable NFS from the "Services" section)

```bash
chown nobody: *path*
```

## Installing

Add the helm repo:

```bash
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner
```

Make sure you know the NFS share IP and path

Installing:

```bash
helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner -n kube-system \
    --set nfs.server=192.168.1.120 \
    --set nfs.path=/mnt/data/kubedata
```
