---
layout: simple-page
title: Containers
permalink: /
---

The Container Ecosystem team has a charter to explore and engage with
emergent projects in server and cloud technology around how they might benefit
or integrate with Juju, particularly in the solution space.

## The people

### Core members

|     | github | twitter | email | website |
|:---:| ------ | ------- | ----- | ------- |
![cute](http://gravatar.com/avatar/122d53411de1158f8b333409da91aa39.jpg?s=25) | [chuckbutler](http://github.com/chuckbutler) | @[lazypower](https://twitter.com/lazypower) | [email](mailto:charles.butler@canonical.com) | [dasroot.net](http://dasroot.net)
![cute](http://gravatar.com/avatar/94805fb3d3bd48e239ec0d15aac00680.jpg?s=25) | [mbruzek](http://github.com/mbruzek) | @[mattatcanonical](https://twitter.com/mattatcanonical) | [email](mailto:matthew.bruzek@canonical.com) | [bruzer.net](http://bruzer.net)

### Honorary members

 * [cloudguru](https://github.com/cloudguru-bb)
 * [lukasa](https://github.com/lukasa)
 * [magicaltrout](https://github.com/buggtb)
 * [whitmo](http://github.com/whitmo)
 * [wwitzellIII](https://github.com/wwitzel3)


You can find us most days on Freenode irc at #Juju.

# Juju Charmer Summit 2016

If you're attending the Juju Charmer Summit in Pasadena CA, this is the section for you!


### Installing Juju

You've probably already installed Juju eiher in the main track, or came with
prior knowledge. If not, there are instructions for:

- [Ubuntu](https://jujucharms.com/docs/stable/getting-started-general#1.-install-juju)
- [MacOS](https://jujucharms.com/docs/stable/reference-releases)
- [Windows](https://jujucharms.com/docs/stable/reference-releases)

You'll likely want to install the 2.0 release, so you can leverage the best of
the new features. We dont recommend placing production deployments on juju 2.0
just yet.

### Your first docker based charm

There have been a few articles published about charming with docker and layers.
I'll assume you're familiar with charm-tools and ready to get started charming
with layer-docker.

Start with the [Layer-Docker Deep Dive](http://dasroot.net/posts/2016-08-03-layer-docker-deep-dive/)


### Advanced Container Deployments

If you're less interested in creating docker based charms and just want to
kick the tires of a container scheduler/manager - give our Kubernetes bundle
a go

`juju deploy canonical-kubernetes`


If you have any further questions, I'm happy to lend a hand. Come find me
in the orange shirt :)

- lazy

## Projects

A list of projects to follow

### Layers & Libraries

#### [Docker Layer](http://github.com/juju-solutions/layer-docker)
  A charm layer for use in the `charm build` process to provide Docker, its principal tooling (docker-compose), and maintain an up-to-date docker daemon on the unit.

#### [Flannel Layer](http://github.com/chuckbutler/layer-flannel)
  Flannel is an overlay network developed by CoreOS. This particular charm layer
  makes use of the Docker Layer, and delivers Flannel in a bootstrap docker
  instance to configure docker networking on the host, delivered from an
  app container, to effect change on the workload-runtime docker
  on the unit.

#### [Kubernetes Layer](http://github.com/mbruzek/layer-k8s)
  Kubernetes is a container orchestrator and scheduler. This layer is
  built on top of the Docker Layer. This layer currently launches both
  leader and worker nodes to each unit. This is a rewrite from the existing
  k8's charm which does bin on host delivery to delivering K8s via docker
  containers. It also ships with SkyDNS and Cadvisor visualization addons

#### [charms.docker Library](http://github.com/juju-solutions/charms.docker)
  `charms.docker` provides charm authors a python library with a clean and readable way to interface with
  the docker CLI as well as configure the Docker deamon via the DockerOpts manager.

  [Documentation](http://pythonhosted.org/charms.docker)

#### [Etcd Layer](https://github.com/chuckbutler/layer-etcd)

Etcd is a key/value store created by CoreOS and is used in several application-container
based solutions, such as Kubernetes. This layer encapsulates the knowledge the
~containers team has working with etcd and delivers a stable healthy etcd cluster.


### Charms and Bundles:

#### Kubernetes bundle
<div class="md-card-container left condensed">
  <div class="juju-card" data-id="~containers/bundle/kubernetes-core"></div>
</div>

The kubernetes-bundle allows you to deploy the many services of Kubernetes to a cloud environment and get started using the Kubernetes technology quickly.

Resources:

[Charm Store](https://jujucharms.com/u/containers/kubernetes-core/)  
[Source code](https://github.com/kubernetes/kubernetes/tree/master/cluster/juju/bundles)  
[Kubernetes Layer](https://github.com/juju-solutions/kubernetes/tree/juju-release-v1.4.0)


#### Observable Kubernetes

<div class="md-card-container left condensed">
  <div class="juju-card" data-id="~containers/bundle/observable-kubernetes"></div>
</div>

Deploy Kubernetes-core hooked into an ELK cluster to aggregate all your container
workload logs. Mine and visualize your container infrastructure log messaging with
Kibana4.

Resources:
[Charm Store](https://jujucharms.com/u/containers/observable-kubernetes)


#### ELK Stack bundle
<div class="md-card-container left">
  <div class="juju-card" data-id="~containers/bundle/elk-stack"></div>
</div>

The Elastic Stack — that's Elasticsearch, Logstash, Kibana — are open source
projects that help you take data from any source, any format and search,
analyze, and visualize it in real time.

This bundle deploys the core services that comprise the ELK stack.

Resources:
[Charm Store](https://jujucharms.com/u/containers/elk-stack)
[Source code](https://github.com/juju-solutions/bundle-elk-stack)

#### Consul charm
<div class="md-card-container left">
  <div class="juju-card" data-id="~containers/trusty/consul"></div>
</div>

Consul is a tool for discovering and configuring services. This charm deploys
a Consul server instance to a public cloud that join with other Consul servers
to form a fully functioning cluster.

Features include: Service Discovery, Health Checking, Key/Value Store, and Multi Datacenter

Resources:

[Source code](https://github.com/mbruzek/consul-charm.git)

#### Etcd charm
<div class="md-card-container left">
  <div class="juju-card" data-id="etcd"></div>
</div>

Etcd is a highly available distributed key value store that provides a reliable
way to store data across a cluster of machines. Etcd gracefully handles master
elections during network partitions and will tolerate machine failure,
including the master.

Resources:
[Charm Store](https://jujucharms.com/u/containers/etcd)
[Etcd Layer](https://github.com/chuckbutler/layer-etcd.git)

#### Drone Charm
<div class="md-card-container left">
  <div class="juju-card" data-id="~lazypower/trusty/drone"></div>
</div>

Drone is a continuous integration platform built on Docker, written in Golang.

This charm will deploy a single Drone CI server to execute builds against your
git repositories hosted by either: GitHub, GitLab, Gogs, or BitBucket.

Drone CI has a flexible job configuration via a single `.drone.yml` include in
your repository. For more information, see the
[upstream documentation](https://github.com/drone/drone/blob/v0.2.1/README.md#builds).

Resources:  
[Source code](https://github.com/chuckbutler/drone-ci-charm)


#### Docker NGINX Charm

an example for charming with docker by leverage an existing docker container of your service, and deploy it with a Juju charm.

Resources:  
[Source code](https://github.com/chuckbutler/docker-nginx-charm)


### Older Deprecated Work


#### DNS Charm
<div class="md-card-container left">
  <div class="juju-card" data-id="~zoology/trusty/dns"></div>
</div>

The DNS charm is unique in that it wraps several other services to provide a
common gateway to automatically provisioning your DNS configuration. Regardless
if you are setting up a BIND cluster, PowerDNS, or integrating with a third
party provider (such as Amazon Rt53, or GoDaddy).

By default the charm will deploy a configured Bind9 server, assuming it is
the authoritative master of the configured domain(s).

Specific instructions how to extend/add providers is outlined in
[docs/HACKING.md](https://api.jujucharms.com/charmstore/v4/~zoology/trusty/dns/archive/docs/HACKING.md)

Resources:  
[Source code](https://github.com/chuckbutler/dns-charm.git)



#### Registrator Charm
<div class="md-card-container left">
  <div class="juju-card" data-id="~zoology/trusty/registrator"></div>
</div>

A subordinate charm enabling charm deployed docker hosts service discovery via etcd or consul.

Resources:  
[Source code](https://github.com/whitmo/registrator-charm)



#### Logspout Charm
<div class="md-card-container left">
  <div class="juju-card" data-id="~containers/trusty/logspout"></div>
</div>

Log shipping for charm deployed docker hosts

Resources:  
[Source code](https://github.com/chuckbutler/logspout-charm)



**DEPRECATED** **[Docker Charm](http://github.com/chuckbutler/docker-charm)** | [Charm Store](https://jujucharms.com/docker/trusty/) <br />
   A charm for deploying a cluster of docker hosts that support extension by charms for service discovery, networking, logging and other fine things.

**DEPRECATED** **[Swarm Charm](http://github.com/whitmo/swarm-charm)**<br />
   A subordinate charm which enables the use of swarm for scheduling and placement onto host deployed with the docker charm

**DEPRECATED** **[Flannel-docker Charm](https://github.com/chuckbutler/flannel-docker-charm)** | [Charm Store](https://jujucharms.com/flannel-docker/trusty/)<br />
   Subordinate charm for SDN for charm deployed docker hosts

**DEPRECATED** **[Calico-docker Charm](https://github.com/chuckbutler/calico-docker-charm)**<br />
   Subordinate charm for SDN for charm deployed docker hosts

**DEPRECATED** **[Hakkasan](https://github.com/chuckbutler/container-dynamics-bundle)**<br />
   Pluggable ad hoc docker orchestration stack solution w/ dns, service discovery and load balancing.


## Collaborating

Want to dive in and hack with us? Interested in writing a charm using docker or lxd? Awesome, check out how where to find us and how to contribute.

- Charm Design doc
- Declared interfaces / data points
- contribution workflow

## The Future: Where is all this going?

We have lots of ideas and would love to hear yours.  Some things we are considering:

 - CI/CD workflows using containers for isolation and moving code through the pipeline.

### Speculative specs

Things we think would be awesome to implement.

- Juju deploy-src: deploy charms and bundles directly from hosted scm
- Mesos/Marathon/Aurora bundle
- Juju provider for Marathon
- Docker machine integration for docker charm

