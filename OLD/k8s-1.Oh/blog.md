# Celebrating Kubernetes 1.0!!!

A big congratulations to the kubernetes project and community from all of us here in Juju land!

Kubernete provides a system for composing containers together to quickly create scalable applications.  The container in k8s acts as a unit of reuse and value.

[To celebrate, We put together a little vodcast about working with k8s 1.0 with juju](embed://video)


## Kubernetes and Juju

We maintain a
[juju bundle](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/cluster/juju/bundles/local.yaml)
as part of the
[kubernetes repository](https://github.com/GoogleCloudPlatform/kubernetes/tree/master/cluster/juju). If
you are interested in hacking on k8s, you can clone the k8s repo, and
deploy your changes to the codebase using juju on a variety of
different clouds: AWS, GCE, Joyent, Digital Ocean, bare metal w/ MaaS
or locally w/ KVM.

> 2015-07-20: For the
> [most current version of the charms, use this branch](https://github.com/chuckbutler/kubernetes/tree/1-oh-sprint/cluster/juju).
> These change will be merged upstream asap.

We also publish this bundle to the Juju charm store so folks can
deploy reliably releases with a more conscise set of commands if you
just want to try out k8s directly from juju.

For either method of deployment, Kubernetes requires some form of dynamic
loadbalancing (ala GCE forwarding rules or AWS ELB) to expose deployed
pods and applications out to the world.


### Deploy Kubernetes 1.0

You'll need to set up juju ([see here for OSX, Ubuntu, or Windows](https://jujucharms.com/get-started) or [here for using docker](http://blog.dasroot.net/2015-unofficial-docker-images.html)).

If you are interested in hacking, [follow these instructions for getting started guide for kubernetes w/ juju](https://github.com/chuckbutler/kubernetes/blob/1-oh-sprint/docs/getting-started-guides/juju.md)

Otherwise you can get k8s deployed with the following command:

  ```juju quickstart -i {{bundle address}}```

The quickstart command will prompt you for your cloud credentials and
bootstraps a juju environment, and then deploys the kubernetes master,
etcd, flannel networking, and two kubernetes minions.

### Configure routing to allow access to applications managed in kubernetes

Kubernetes depends on a system for managing routes such as AWS ELB or
GCE's loadbalancing to expose your containerized services outside of
kubes.  Juju strives to stay cloud agnostic, so currently we need to
configure either GCE or AWS outside of juju to enable access to our
pods and applications.

We think it should be pretty straightforward to create a charm that
could give this ability to any cloud without additional configuration
regardless of where k8s is deployed. An approach that charms
[a reverseproxy and service discovery similar to this](https://github.com/darkgaro/kubernetes-reverseproxy/blob/master/Dockerfile)
should do the trick.  If you are interested in easily running Kubes on
other clouds (or metal) we'd love to collaborate!

## Want to learn more? Interested in contributing? Just want to talk shop?

We'd love to chat! Come talk to us! You can find us on irc on freenode in
#google-containers, #system-zoo, and #juju.

If you are attending the k8s launch party, we'll also be there! Look
for [Whit Morriss](https://twitter.com/whit),
[Antonio Rosales](https://twitter.com/a_webtone) or Alexis Bruemer and
come say hi!
