# Charming with Docker

You have a Docker container and you heard about Juju.  Juju can deploy your
Docker container to any cloud. This document will outline the best practices
for using Juju to deploy Docker images.

### First things first

This document assumes you already know about [Docker](http://docker.com) and
how to create, pull and use application containers.
[Juju](https://jujucharms.com/docs/stable/about-juju) may be a new
concept so you should [get started](https://jujucharms.com/get-started)
with the technology, there is more information on
[installation and configuration](https://jujucharms.com/docs/stable/getting-started)
of Juju software on <https://jujucharms.com>.  This document will detail some of
the higher level [concepts of Juju](https://jujucharms.com/docs/stable/glossary).
<!-- These concepts are new, and as this is an open source product YOU, yes you can
influence the features and direction of these new concepts.
I'm not sure the sales pitch adds anything here. Commenting for now
-->


## Juju

Juju is a model driven, declarative language to define software services and
how they relate with each other. A charm is an encapsulation of the software
install, configuration, and relations. To deliver a Docker image with Juju you
would write a charm that Juju can deploy to any cloud.

### The traditional charming process

The [traditional](https://jujucharms.com/docs/master/authors-charm-writing)
method of creating a Juju charm is to encapsulate all the
install and configuration of a service in what Juju calls
[hooks](https://jujucharms.com/docs/stable/authors-charm-hooks). Juju runs
the associated hook when certain events occur.  The key is to understand the
event paradigm and write hooks that are appropriate for that model.  You will
need to understand these concepts of charming to deliver software with Juju.

### Reactive and composing charms

#### Reactive

Another software paradigm is
[reactive programming](https://en.wikipedia.org/wiki/Reactive_programming). Do
something when the state or conditions are correct. Juju offers the
[charms.reactive](http://pythonhosted.org/charms.reactive/) package to allow
charms to be written in the reactive paradigm. In charms.reactive code
execution is controlled by boolean logic. You can define when the conditions
are right, run this code, or when something is not set, run different code or
do nothing at all.

#### Composition

The idea of composition is to combine objects or data into more complex objects
or data. When applied to Charms, composition allows you to extend or build off
other charms to make more complex or useful charms.  The `compose.yaml` file in
the root directory of the charm controls what layer(s) will be imported.

#### Reactive Charms

The docker charm makes use of the
[charms.reactive](http://pythonhosted.org/charms.reactive/) python framework.
The code for the docker layer can be found in the `reactive/` folder in the
root charm directory.

#### Composing Charms

The docker charm makes use of the
[Charm Composition](https://jujucharms.com/docs/master/authors-charm-composing)
concept building off the base charm and creating its own layer of added
functionality.  The docker charm serves as a base for other charms and allows
people to extend and make docker based charms of their own.

### Ready to get started?

#### layer-docker charm

The layer-docker charm can be found on github.com at:
<https://github.com/juju-solutions/layer-docker>

Again this charm is designed to be a base for other docker charms.  If you want
an example of a charm that extends the layer-docker charm check out the
layer-docker-nginx charm <https://github.com/juju-solutions/layer-docker-nginx>.
