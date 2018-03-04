Jenkins Kubernetes Experiment
=============================

This uses [Helm](https://www.helm.sh/) to spin up a Jenkins instance that's
configured to be secure by default.

Getting started
---------------

You'll need a kubernetes cluster running. There's one built in to docker-for-mac now.

You'll also need to [install the Helm Tiller](https://docs.helm.sh/using_helm/#installing-tiller) into your cluster.

Once you've done that:

```
helm install .
```

Will bring up the cluster.

This can take quite a while, so it's worth going to make a cup of tea or
polling for the pod to become healthy:

```
watch kubectl get pods,svc
```

Helm will give the cluster some random codename (e.g. virtuous sparrow), which
you can see in the name of the pods and services.

Jenkins will come up with a random admin password, which you can ask kubernetes
for so you can log in:

```
printf $(kubectl get secret --namespace default "${cluster_codename}-jenkins" -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
```

