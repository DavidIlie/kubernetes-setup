# Authelia integration

As of right now, the only way to get Authelia functioning is to use a kind of persistent volume from [step 7](https://github.com/DavidIlie/kubernetes-setup/tree/master/7%20-%20nfs%20pvc) so that we can modify the files whenever we want, as you would need to modify it in the future if you want to add more protected routes.

## Prerequisites

You first need to generate a password for your Authelia account by running this docker command below:

```docker
docker run authelia/authelia:latest authelia hash-password *password*
```

Make sure to keep this password while we move on.

## Configuring it to your needs

In the `files/` directory you will see two files, make sure to fill of all these to your configuration, if you use mine it might not work.

In `configuration.yml` under `access_control` you are able to modify which routes should be protected and which shouldn't be. However, `default_policy` allows you to make a default for any ingress that will go through Authelia.

With the password that you generated earlier you can put it the `users_database.yml` file where it shows "password".

## Installing it

With the two files configured, go into the manifests folder, and again, modify them to your needs. My manifests might not work in your setup. With those modified you need to first create the namespace by doing:

```bash
kubectl create -f namespace.yml
```

Now, we need to create the volume:

```bash
kubectl create -f volume.yml
```

With the volume created, navigate to your NFS server and transfer the two files from `files/` to the directory created in the NFS share. If you are having permissions issues, create the files manually directly on the NFS server.

Finally we can install the deployment and service:

```bash
kubectl create -f deployment.yaml -f service.yaml
```

With those created you can now create an Ingress or IngressRoute for authelia to the domain you configured in `files/configuration.yml`.

## Registering the middleware in traefik

You also need to modify the auth page domain in `middleware.yaml` before applying:

```bash
kubectl apply -f middleware.yaml
```

## Creating Ingress Routes

If you take a look in the `examples` folder you can see a IngressRoute I create for a service of mine (Heimdall) running in my cluster. This IngressRoute uses the traefik middleware as i included it in the `middlewares` part of the yaml.

If you don't want to use IngressRoutes and you want to create standard ingresses using Rancher (for example) you need to include this annotation in your labels to identify that the route you are creating is protected by Authelia.

```
traefik.ingress.kubernetes.io/router.middlewares=default-authelia@kubernetescrd
```

This is also added in the [commons](https://github.com/DavidIlie/kubernetes-setup/blob/master/README.md) directory in this repository so that it can be accessed more easily.

## Done!

If all goes well, you should see a page like this when you access a protected page:

<img src="https://user-images.githubusercontent.com/47594764/124361016-0cb8aa80-dc2d-11eb-8f7c-6215b78d2121.png"/>
