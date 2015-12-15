# tupperware: containers and friends w/ Juju

The Canonical new workloads team has a charter to explore and engage with emergent projects in server and cloud technology around how they might benefit or integrate with Juju, particularly in the solution space.

## The new workloads team

Team core members:
- @[chuckbutler](http://github.com/chuckbutler) [ [twitter](https://twitter.com/lazypower)] [ [email](mailto:charles.butler@canonical.com) ] [ [blog](http://blog.dasroot.net) ]
- @[mbruzek](http://github.com/mbruzek) [ [twitter](https://twitter.com/mattatcanonical) ] [ [email](mailto:matthew.bruzek@canonical.com) ] [ [blog](http://bruzer.net) ]

Team honorary members:
 - @[wwitzellIII](https://github.com/wwitzel3)
 - @[lukasa](https://github.com/lukasa)
 - @[whitmo](http://github.com/whitmo) [ [twitter](https://twitter/whit) ]

You can find us most days on freenode irc at #system-zoo or #Juju.

### UOS Announced projects for the current cycle

[Watch the UOS 1115 session w/ the New Workloads team](https://youtu.be/S7xUVKCWAXU)

#### Projects to watch:

**[Docker Layer](http://github.com/juju-solutions/layer-docker)** | <br/>
  A charm layer for use in the `charm build` process to provide Docker, its principal tooling (docker-compose), and maintain an up-to-date docker daemon on the unit.

**[Flannel Layer](http://github.com/chuckbutler/layer-flannel)** | <br/>
    Flannel is an overlay network developed by CoreOS. This particular charm layer
    makes use of the Docker Layer, and delivers Flannel in a bootstrap docker
    instance to configure docker networking on the host, delivered from an
    app container, to effect change on the workload-runtime docker
    on the unit.

**[Kubernetes Layer](http://github.com/mbruzek/layer-k8s)** | <br/>
    Kubernetes is a container orchestrator and scheduler. This layer is
    built on top of the Docker Layer. This layer currently launches both
    leader and worker nodes to each unit. This is a rewrite from the existing
    k8's charm which does bin on host delivery to delivering K8s via docker
    containers. It also ships with SkyDNS and Cadvisor visualization addons

**[Charms.Docker](http://github.com/juju-solutions/charms.docker)** | <br/>
    `charms.docker` provides charm authors a python library with a clean and readable way to interface with
    the docker CLI as well as configure the Docker deamon via the DockerOpts manager.

### Projects of note:

**[Kubernetes bundle](https://github.com/kubernetes/kubernetes/tree/master/cluster/juju/bundles)** | [Charm Store](https://jujucharms.com/u/kubernetes/kubernetes-cluster/)<br />
   a configurable multi-cloud solution for deploying and managing k8s that runs atop the docker charm to provide scheduling and loadbalancing for docker containers.

**[Consul charm](https://github.com/mbruzek/consul-charm.git)**<br />
  Deploy and manage a consul cluster

**[Etcd charm](https://github.com/chuckbutler/etcd-charm.git)**<br />
  Deploy and manage an etcd cluster

**[Drone Charm](https://github.com/chuckbutler/drone-ci-charm)**<br />
  CI/CD solution for containers


**[DNS Charm](https://github.com/chuckbutler/dns-charm.git)**<br />
  Manage and "orchestrate" your DNS via a polymorphic service charm. Supports
  offline installation to provide a Bind9 authoritative master, or proxy requests
  to your DNS provider of choice. Illustrates embedding a plugin architecture into
  charms, complete with Dependency management and testing structure.

**[Docker NGINX Charm](https://github.com/chuckbutler/docker-nginx-charm)**<br />
  (an example for charming with docker) Leverage an existing docker container of your service, and deploy it with a Juju charm.

**[Registrator Charm](https://github.com/whitmo/registrator-charm)**<br />
   A subordinate charm enabling charm deployed docker hosts service discovery via etcd or consul.

**[Logspout Charm](https://github.com/chuckbutler/logspout-charm)**<br />
   Log shipping for charm deployed docker hosts

#### **Depreciated / Classic charms**

**DEPRECATED** **[Docker Charm](http://github.com/chuckbutler/docker-charm)** | [Charm Store](https://jujucharms.com/docker/trusty/) <br />
   A charm for deploying a cluster of docker hosts that support extension by charms for service discovery, networking, logging and other fine things.

**DEPRECATED** **[Swarm Charm](http://github.com/whitmo/swarm-charm)**<br />
   A subordinate charm which enables the use of swarm for scheduling and placement onto host deployed with the docker charm



**[Flannel-docker Charm](https://github.com/chuckbutler/flannel-docker-charm)** | [Charm Store](https://jujucharms.com/flannel-docker/trusty/)<br />
   Subordinate charm for SDN for charm deployed docker hosts

**DEPRECATED** **[Calico-docker Charm](https://github.com/chuckbutler/calico-docker-charm)**<br />
   Subordinate charm for SDN for charm deployed docker hosts

**[Hakkasan](https://github.com/chuckbutler/container-dynamics-bundle)**<br />
   Pluggable ad hoc docker orchestration stack solution w/ dns, service discovery and load balancing.




#### Fun projects:

- [System Zoo](http://github.com/systemzoo)
  * sound system ops dj (Dockercon Hackathon Project) - Canary feedback system for rolling out dockerized web apps

Supporting tools and charms



#### Exprimental Tooling/Charms:

These charms/tools were created to experiment with the ecosystem and make assertions
about the tooling we are delivering, and how to best ulitilze/leverage the
infrastructure in a user friendly manner.

- [Docker Build Hook Charm](https://github.com/chuckbutler/docker-build-hook-charm)
    Provides webhooks for building a docker-container on push, and immediate
    recycling of the service. PHAUX PAAS delivery of DOCKERFILES on top of juju.
- [Dockerfile Charm](https://github.com/chuckbutler/dockerfile-charm)
    Deploy any repository from a Dockerfile, works hand in hand with the docker-build-hook charm
- [Docker Compose Charm](https://github.com/chuckbutler/docker-compose-charm)
    Deploy any application into the Juju Docker infrastructure that contains a
    `docker-compose.yaml` file, to easily spin up all dependent services.
- [Squid Deb Proxy Charm](https://github.com/chuckbutler/squid-deb-proxy-charm)
    Cache APT sources in an environment (on the same subnet) and distribute
    locally to speed up deployments/updates across a large cluster of services.

**Service process handling for charms**<br />
Juju native plugins for handling container runtimes and other long running processes


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

## Interested in Systems and workloads?

 System Zoo is a community gathering of people driving and exploring
interesting workloads. We accept dabblers and hackers of all walks of life in
development, ops, networking, social engineering, etc. If you're doing something
interesting, we'd love to chat!

 You can find us in [#system-zoo](https://webchat.freenode.net/?channels=system-zoo)
on irc.freenode.net, with an upcoming schedule of media, podcasts, and blog
forthcoming as time allows.
