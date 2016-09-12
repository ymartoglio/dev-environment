MongoDB image
=============
Based on ubuntu 16.04

https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
Community edition

```
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927

RUN echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

RUN apt-get update
RUN apt-get install -y mongodb-org

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]
```

Build
-----
```bash
$ cd /path/to/Dockerfile/
$ docker build -t yo/mongo .
```

Run
---
```bash
$ cd /path/to/Dockerfile/
$ docker run -v $PWD/data:/data -p 27017:27917 --net dev-bridge --ip 10.10.0.2 -it yo/mongo
```
 * Mount the data folder so the data persists in the host's system
 * Folder tree must be `/data/db`
 * The virtual system exposes the mongodb default connection port `27017` and the running container binds it to host's port `27017`
