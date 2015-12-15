# Charming with Docker

> This is a guideline reference for planning the docker charming tutorial
> and makes some assumptions about the introduction of the technology, plus
> stack of tech that will be used to create these charms.
>
> Any user coming into this ecosystem is assumed to understand how to create
> docker images, but have no understanding of juju charming.


## A narrative view into consuming Docker with Juju Charms



#### Introduce Charm Compose

Basic introductin to composer, features it adds, and value proposition

#### Intoduce Charm layer 2

Layer on basic deployable docker container, using a classic webapp example

#### Introduce Juju Process Management registration

Add process management metdata to metadata.yaml (will move to proces.yaml)

add hooks:
  Launch process using process-launch <foo>

#### Wrap up of composed charm w/ process management

Launch process and surface information in juju status

#### Introduce configuration

add statically deployable site configuration

Add hook code to handle site configuration and register/deregister based
on configuration

#### Illustration of configuration

Show examples / screenshots of deployment example w/ configuration and
behavior changes

#### Introduction of relationships w/ docker based charms

Cover relationship model, link to docs for more information.

Write code friendly for relationship stubs, and illustrate relationship
with a load balancer

#### Summary of basic charm development w/ composer


#### Introduction of Reactive Pattern and Composer

Introduce reactive charm framework

re-compose above illustration in reactive framework, and relation
stubs w/ a local archive example

#### summary of reacive charm w/ relation stubs

contrast/compare original charm vs reactive charm + stubs and reduced
maintenance overhead

> The following are ammendment sections that authors will likely have
> questions over, and we can provide in a FAQ style document to start
> dialogue, to iterate and break into additional sections later

#### In depth with docker options and considerations when charming

env vars, volume mapping, and networking concerns
