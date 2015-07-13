# tupperware: containers and friends w/ Juju

The Canonical new workloads team has a charter to explore and engage with emergent projects in server and cloud technology around how they might benefit or integrate with juju, particularily in the solution space.

## The new workloads team

Team core members:
- @chuckbutler
- @mbruzek
- @whitmo 
 * [twitter](https://twitter/whit)
 * [email](mailto:whit.morriss@canonical.com)
 * [blog](http://bfh.whitmorriss.org)

Team honorary members:
 - @wwitzellIII

You can find us most days on freenode irc at #system-zoo or #juju.

Projects of note:

- Docker Charm & Friends
 - Docker Charm
   A charm for deploying a cluster of docker hosts that support extension by charms for service discovery, networking, logging and other fine things. 
 - Swarm Charm 
   A subordinate charm which enables the use of swarm for scheduling and placement onto host deployed with the docker charm
 - Registrator Charm
   A subordinate charm enabling charm deployed docker hosts service discovery via etcd or consul.
 - Logspout Charm
   Log shipping for charm deployed docker hosts
 - Flannel-docker Charm
   Subordinate charm for SDN for charm deployed docker hosts
 - Calico-docker Charm
   Subordinate charm for SDN for charm deployed docker hosts
 - Kubernetes bundle
   a configurable multi-cloud solution for deploying and managing k8s that runs atop the docker charm to provide scheduling and loadbalancing for docker containers.
 - Hakkasan 
   Pluggable ad hoc docker orchestration stack solution w/ dns, service discovery and load balancing.
- Consul charm
  Deploy and manage a consul cluster
- Etcd charm
  Deploy and manage an etcd cluster
- Drone Charm
  CI/CD solution for containers

- Charm processes - juju native plugins for handling container runtimes and other long running processes
 

Fun projects:
 - System Zoo
  * sound system ops dj (Dockercon Hackathon Project) - Canary feedback system for rolling out dockerized web apps
 
Supporting tools and charms

- AnsibleCharm - library for facilitating the authoring of charms using ansible.

 
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

- juju deploy-src: deploy charms and bundles directly from hosted scm
- Mesos/Marathon/Aurora bundle
- Juju provider for Marathon
- Terraform provider that drives a Juju environment
- Docker machine integration for docker charm




