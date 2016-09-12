NodeJS image
============
ubuntu 16.04
node v6.x

**src/package.json** - application minimal pour la vérification du bon fonctionnement (https://docs.docker.com/engine/examples/nodejs_web_app/)

Packages
--------
 * nodemon for auto reload when sources changed
 * bower for clientside dependencies

```
RUN apt-get update

#node 6 install
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

RUN npm install -g bower
RUN npm install -g nodemon
RUN ln -s /usr/bin/nodejs /usr/bin/node
```

Share app source from localhost folder
----------------------------------------
with docker run -v option

Build
-----
```bash
$ cd /path/to/Dockerfile/
$ docker build -t yo/node .
```

Run
---
```bash
 $ cd /path/to/my/Dockerfile
 $ docker run -v $PWD/app:/app --net dev-bridge --ip 10.10.0.1 -it yo/node
```

At startup the containers execute the entrypoint shell parameters :

The container will expose `8080` and `5858`

```
# install & launch the app
ENTRYPOINT cd /app;npm install --development;nodemon /app/src/server.js
```

`nodemon` auto launch on source file updated
