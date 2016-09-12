MUST KNOW
=========


- **image** : minimal vm built with system and package installed (described by a **Dockerfile**)
- **container** : a running images

Dockerfile
==========

 - **FROM**

    Choose os

 - **RUN**

    Run a shell command duriong image building

 - **EXPOSE**

    Expose a **port** (can be redirected to host port by docker run -v option)

 - **ENTRYPOINT**

    Only one `ENTRYPOINT` by file

 - **CMD**

    Only one `CMD` by file, may be overrided by command line docker run param.



Basics commands
===============

docker help
docker <cmd> --help

Build images
------------
```bash
$ cd /my/docker/file/folder
$ docker build --tag yo/node-test .
```

Run images
----------
```bash
    $ docker run  -it <repo>/<name>
```
Options

    -p <localport>:<exposedport>
    -i outputs redirected to stdout
    -t open a pseudo-tty
    -v mount volume in container
    --name <not_funny_name>
    --net <name_of_a_bridge>

Mounted file with **docker run -v**


For containers
--------------
Display container data as table

```bash
    $ docker ps
```

Options
    -a all
    -q only display container's ID which is nice for maintenance tasks


For images
----------
Display images data as table

```bash
    $ docker images
```

Options

    -a also display images tagged with none
    -f filter

Filter with grep (first column is the container id)

    $ docker ps -a | grep 'something' | awk '{print $1}'


Maintains environment
=====================

For containers
--------------
Remove container
```bash
    $ docker rm $(docker ps)
```

Check containers connected to `bridge`

```bash
    $ docker network inspect bridge
```
(https://docs.docker.com/engine/userguide/networking/dockernetworks/)


For images
----------

Remove all untagged images

```bash
    $ docker rmi $(docker images -a | grep '<none>' | awk '{print $3}')
```
or
```bash    
    $ docker images -a | grep '<none>' | awk '{print $3}' | xargs docker rmi
```


Network configuration
=====================

Container
---------
To specify an ip with `run` `--ip` option, the container must be connected to a custom bridge
with `--net`.
(https://docs.docker.com/engine/userguide/networking/dockernetworks/#user-defined-networks)


Create bridge
-------------

`dev-bridge`

```bash
 # Create the bridge
 $ docker network create \
    --driver=bridge \
    --subnet=10.10.0.0/24 \
    --gateway=10.10.0.254 dev-bridge
 # Display info
  $ docker network inspect dev-bridge    
```


Daemon
------
When installed, docker creates a default bridge named `docker0` width default subnet configuration.
to override subnet default, use `--bip` options on the docker's daemon startup.

Modify the startup options by adding `--bip`

```
 /usr/bin/docker --bip=2.2.0.1/24
 # host bridge IP/netmask 255.255.255.0
```



Daemon startup options
======================


On SysVInit sevice manager
--------------------------
edit `/etc/default/docker`

```bash
$ vim /etc/default/docker
#Override the DOCKER_OPTS constant
```

On systemd service manager
--------------------------
Create a text file named `docker` in `/etc/default`
(or in `/etc/systemd/system/docker.service.d/<something>.conf` for systemd only)
```bash
$ vim /etc/default/docker
# ADD DOCKER_OPTS="<options you want>"
```

Edit `/lib/systemd/system/docker.service`
Modify the `[Service]` section by adding the config file and updating the ExecStart constant




```bash
   $ vim  /lib/systemd/system/docker.service

   [Service]
   EnvironmentFile=/etc/default/docker
   ExecStart=/usr/bin/docker $DOCKER_OPTS -H fd://
```
