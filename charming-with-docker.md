# Charming with Docker
You have a Docker container and you heard about Juju.  Juju can deploy your
Docker container. This document will outline the best practices for using Juju
to deploy Docker images.

## Assumptions
This document assumes you already know about [Docker](http://docker.com) and
how to create, pull and use containers.
[Juju](https://jujucharms.com/docs/stable/about-juju) may be a new
concept so you should [get started](https://jujucharms.com/get-started)
with the technology, there is more information on
[install and configuration](https://jujucharms.com/docs/stable/getting-started)
of the Juju software on <https://jujucharms.com>.  This document will be
detail some of the higher level
[concepts of Juju](https://jujucharms.com/docs/stable/glossary).  These
concepts are new, and as this is an open source product YOU, yes you can
influence the features and direction of these new concepts.

## Juju
Juju is a model driven, declarative language to define software services and
how they relate with each other. A charm is an encapsulation of the software
install, configuration, and relations. To deliver a Docker image with Juju you
would write a charm that Juju can deploy to any cloud.

### The traditional charming process
The traditional way of creating a Juju charm is to encapsulate the all the
install and configuration of a service in what Juju calls
[hooks](https://jujucharms.com/docs/stable/authors-charm-hooks). You will need
to understand the concepts of charming to deliver software with Juju.

### The new charming process
The concept of building off of other things is nothing new.  The idea of
compsing
