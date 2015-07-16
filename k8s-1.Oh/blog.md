# Celebrating Kubernetes 1.0!!!

A big congratulations to the kubernetes project and community from all of us here in Juju land!

Kubernete provides a system for composing containers together to quickly create scalable applications.  The container in k8s acts as a unit of reuse and value.

## Kubernetes and Juju

We maintain a [juju bundle]() as part of the [kubernetes repository](). If you are interested in hacking on k8s, you can clone the k8s repo, and deploy your changes to the codebase using juju on a variety of different clouds: AWS, GCE, Joyent, Digital Ocean, or locally w/ KVM.

You'll need to set up juju ([see here for ubuntu native setup]() or [here for using docker]()).  Then you can hack and launch k8s using the cluster directory semantics common to the project.

```
local hacking example
```

We also publish this bundle to the Juju charm store so folks can deploy reliably releases with a more conscise set of commands (if you just want to try out k8s):

  ```juju quickstart {{bundle address}}```
