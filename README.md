# tupperware: containers and friends w/ Juju

The Canonical new workloads team has a charter to explore and engage with emergent projects in server and cloud technology around how they might benefit or integrate with Juju, particularily in the solution space.

## The new workloads team

Team core members:
- @[chuckbutler](http://github.com/chuckbutler) [ [twitter](https://twitter.com/lazypower)] [ [email](mailto:charles.butler@canonical.com) ] [ [blog](http://blog.dasroot.net) ]
- @[mbruzek](http://github.com/mbruzek) [ [twitter](https://twitter.com/mattatcanonical) ] [ [email](mailto:matthew.bruzek@canonical.com) ] [ [blog](http://bruzer.net) ]
- @[whitmo](http://github.com/whitmo) [ [twitter](https://twitter/whit) ] [ [email](mailto:whit.morriss@canonical.com) ] [ [blog](http://bfh.whitmorriss.org) ]

Team honorary members:
 - @[wwitzellIII](https://github.com/wwitzel3)
 - @[lukasa](https://github.com/lukasa)

You can find us most days on freenode irc at #system-zoo or #Juju.

#### Projects of note:

- Docker Charm & Friends
 - [Docker Charm](http://github.com/chuckbutler/docker-charm)
   A charm for deploying a cluster of docker hosts that support extension by charms for service discovery, networking, logging and other fine things. 
 - [Swarm Charm](http://github.com/whitmo/swarm-charm)
   A subordinate charm which enables the use of swarm for scheduling and placement onto host deployed with the docker charm
 - [Registrator Charm](https://github.com/whitmo/registrator-charm)
   A subordinate charm enabling charm deployed docker hosts service discovery via etcd or consul.
 - [Logspout Charm](https://github.com/chuckbutler/logspout-charm)
   Log shipping for charm deployed docker hosts
 - [Flannel-docker Charm](https://github.com/chuckbutler/flannel-docker-charm)
   Subordinate charm for SDN for charm deployed docker hosts
 - [Calico-docker Charm](https://github.com/chuckbutler/calico-docker-charm)
   Subordinate charm for SDN for charm deployed docker hosts
 - [Kubernetes bundle](https://github.com/GoogleCloudPlatform/kubernetes/tree/master/cluster/Juju/bundles)
   a configurable multi-cloud solution for deploying and managing k8s that runs atop the docker charm to provide scheduling and loadbalancing for docker containers.
 - [Hakkasan](https://github.com/chuckbutler/container-dynamics-bundle)
   Pluggable ad hoc docker orchestration stack solution w/ dns, service discovery and load balancing.
 - [Consul charm](https://github.com/mbruzek/consul-charm.git)
  Deploy and manage a consul cluster
 - [Etcd charm](https://github.com/chuckbutler/etcd-charm.git)
  Deploy and manage an etcd cluster
 - [Drone Charm](https://github.com/chuckbutler/drone-ci-charm)
  CI/CD solution for containers
 - [DNS Charm](https://github.com/chuckbutler/dns-charm.git)
  Manage and "orchestrate" your DNS via a polymorphic service charm. Supports
  offline installation to provide a Bind9 authoritative master, or proxy requests
  to your DNS provider of choice. Illustrates embedding a plugin architecture into
  charms, complete with Dependency management and testing structure.
 - [Docker NGINX Charm](https://github.com/chuckbutler/docker-nginx-charm)
  (an example for charming with docker) Leverage an existing docker container of your service, and deploy it with a Juju charm.

- Charm processes - Juju native plugins for handling container runtimes and other long running processes


#### Fun projects:

- [System Zoo](http://github.com/systemzoo)
  * sound system ops dj (Dockercon Hackathon Project) - Canary feedback system for rolling out dockerized web apps

Supporting tools and charms

- [AnsibleCharm](https://github.com/whitmo/ansible-charm) - library for facilitating the authoring of charms using ansible.


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
- Terraform provider that drives a Juju environment
- Docker machine integration for docker charm

## Interested in Systems and workloads?

 System Zoo is a community gathering of people driving and exploring
interesting workloads. We accept dabblers and hackers of all walks of life in
development, ops, networking, social engineering, etc. If you're doing something
interesting, we'd love to chat!

 You can find us in [#system-zoo](https://webchat.freenode.net/?channels=systemzoo)
on irc.freenode.net, with an upcoming schedule of media, podcasts, and blog
forthcoming as time allows.




