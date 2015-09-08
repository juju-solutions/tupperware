# Charm authoring using reactive paradigm

The [charms.reactive](http://pythonhosted.org/charms.reactive/) is a python
module to bring the
[reactive programming](https://en.wikipedia.org/wiki/Reactive_programming)
pattern to Juju charms. We call this "reactive" because code can be executed
when certain conditions exist, as if the code is reacting to those conditions.
For the most complete information on charms.reactive go to
<http://pythonhosted.org/charms.reactive/>

## layer-docker charm
An example of a charm using the reactive pattern is the
[layer-docker charm](https://github.com/juju-solutions/layer-docker).
It also uses the compose workflow and can serve as the base for other Docker
charms.  This document will focus on the reactive parts of the layer-docker
charm.  If you want to read more about compose in the Juju
[composing documentation](https://jujucharms.com/docs/devel/authors-charm-composing).

```
├── composer.yaml
├── metadata.yaml
├── reactive
│   └── docker.py
├── README.md
└── scripts
    └── install_docker.sh
```

### The reactive directory
Making a charm "reactive" adds two directories (`reactive` and `relations`)
to the basic charm structure. The layer-docker charm only has a `reactive`
directory because it does not add (or provide) any new relations.

Inside the `reactive` directory there is a file `docker.py`.  The reactive
framework goes into the reactive directory and finds the `docker.py` file.

```python
@hook('install')
def install():
    hookenv.status_set('maintenance', 'Installing Docker and AUFS')
    charm_path = path(os.environ['CHARM_DIR'])
    install_script_path = charm_path/'scripts/install_docker.sh'
    check_call([install_script_path])
    hookenv.status_set('active', 'Docker Installed')
    reactive.set_state('docker.available')
```

The file contains a single function named "install" which has a decorator
`@hook` indicating this function should be called on the `install` event. The
reactive framework handles hooks in a special way.  All the hooks of the same
name will be run in a non-determinded order, so generally only one layer should
implement a hook for best results.  

This install hook creates a path to an install script and calls the script to
install Docker.  After Docker installs it calls the reactive `set_state`
method.  This method puts the "docker.available" state in the reactive
framework so that other layers know that Docker is installed and available.

The layer-docker charm is a great example of how small and focused a charm can
be when it uses reactive and compose concepts.

## States

States can be though of as persistent events.  The code using the reactive
framework can set and remove states. Other code known as handlers can use the
boolean logic to run when the state or combination of states is correct. States
may be useful to other layers so it is very important to document in the
`README.md` what states are set or removed in this layer.

<a name="layer-docker-nginx"></a>
## layer-docker-nginx
The layer-docker-nginx charm adds the [Nginx](http://nginx.org/) HTTP server
docker image to the layer-docker charm by using `charm compose` and also uses
the reactive framework.  The
[layer-docker-nginx charm](https://github.com/juju-solutions/layer-docker-nginx)
can be found on github.

## The reactive directory
Inside the reactive directory of the layer-docker-nginx charm is a file
`nginx.py` that contains all the code for this charm.  

```
├── assets
│   ├── index.html
│   └── jujuanddocker.png
├── composer.yaml
├── config.yaml
├── copyright
├── metadata.yaml
├── notes.md
├── reactive
│   └── nginx.py
└── README.md
```

### Standard hook function
The `nginx.py` file contains a "config-changed" hook that is called when
someone changes a configuration value in Juju. This function uses charmhelpers
to determine if the port has changed and the container needs to be recycled.

## Reactive functions
The `nginx.py` file contains several functions that make use of the reactive
framework.  The `@when` and `@when_not` are
[charms.reactive decorators](http://pythonhosted.org/charms.reactive/charms.reactive.decorators.html).
The decorated functions are only run if the conditions match the current state.
The functions described here are specific to the nginx workload, but the
concepts can be extended to the other Docker worklodas to write your own charm
with the layer-docker charm as the base.

#### install_nginx
The layer-docker charm sets the "docker.available" state after installing and
configuring Docker.  The `install_nginx` function is decorated with
`@when('docker.available')` meaning that the code will run after Docker is
installed and configured.  The install_nginx function sets the state
"nginx.available" when it is complete.
```python
@when('docker.available')
def install_nginx():
    '''
    Default to only pulling the image once. A forced upgrade of the image is
    planned later. Updating on every run may not be desireable as it can leave
    the service in an inconsistent state.
    '''
    if reactive.is_state('nginx.available'):
        return
    copy_assets()
    hookenv.status_set('maintenance', 'Pulling Nginx image')
    check_call(['docker', 'pull', 'nginx'])
    reactive.set_state('nginx.available')
```

#### run_container
This function handles running the nginx container which many Docker charms
will have to do.  The run_container function is decorated with two decorators
`@when('nginx.available', 'docker.available')` and `@when_not('nginx.started')`.
The `@when` decorator indicates the desired states and both must be set before
the run_container function is executed.  The `@when_not` decorator indicates
the state that must not be active for this function to run. Since the
run_container function sets the "nginx.started" state this ensures the
container is not started over and over again.
```python
@when('nginx.available', 'docker.available')
@when_not('nginx.started')
def run_container(webroot=None):
    '''
    Wrapper method to launch a docker container under the direction of Juju,
    and provide feedback/notifications to the end user.
    '''
    if not webroot:
        webroot = config['webroot']
    # Run the nginx docker container.
    run_command = [
        'docker',
        'run',
        '--restart',
        'on-failure',
        '--name',
        'docker-nginx',
        '-v',
        '{}:/usr/share/nginx/html:ro'.format(webroot),
        '-p',
        '{}:80'.format(config['port']),
        '-d',
        'nginx'
    ]
    check_call(run_command)
    hookenv.open_port(config['port'])
    reactive.remove_state('nginx.stopped')
    reactive.set_state('nginx.started')
    hookenv.status_set('active', 'Nginx container started')
```

#### stop_container
The stop_container function is decorated with
`@when('nginx.stop', 'docker.available')`.  The "nginx.stop" state is an
indication to stop the container in which case it will set the "nginx.stopped"
state. The decorator `@when_not('nginx.stopped')` protects this function from
being called repeatedly. Note the `reactive.remove_state('nginx.stop')` and
`reactive.set_state('nginx.stopped')`calls to assert a stopped state.
```python
@when('nginx.stop', 'docker.available')
@when_not('nginx.stopped')
def stop_container():
    '''
    Stop the NGinx application container, remove it, and prepare for launching
    of another application container so long as all the config values are
    appropriately set.
    '''
    hookenv.status_set('maintenance', 'Stopping Nginx container')
    # make this cleaner
    try:
        check_call(['docker', 'kill', 'docker-nginx'])
    except:
        pass
    try:
        check_call(['docker', 'rm', 'docker-nginx'])
    except:
        pass
    reactive.remove_state('nginx.started')
    reactive.remove_state('nginx.stop')
    reactive.set_state('nginx.stopped')
    hookenv.status_set('waiting', 'Nginx container stopped')
```

#### configure_website_port
The configure_website_port is a function that handles the http relationship,
specifically the port. This function is decorated with
`@when('nginx.started', 'website.available')` to only run when Nginx is started
and the website is available.

```python
@when('nginx.started', 'website.available')
def configure_website_port(http):
    '''
    Relationship context, used in tandem with the http relation stub to provide
    an ip address (default to private-address) and set the port for the
    relationship data
    '''
    serve_port = config['port']
    http.configure(port=serve_port)
    hookenv.status_set('active', '')
```

## Now write your own compose and reactive charm

The [layer-docker charm](https://github.com/juju-solutions/layer-docker) was
designed to be a base layer for other charms that need to do Docker things. By
using the reactive framework the charms that you write can be very small and
concentrate on the service or services that your charm provides.  Use the
compose workflow and reactive framwork to create a new charm with your Docker
image very similar to the [layer-docker-nginx](#layer-docker-nginx) charm.
