dev-env docker's images
=======================


Network
=======
Custom network bridge `dev-bridge` created to enclose the development environment's capabilities
```bash
 $ docker network create --driver=bridge --subnet=10.10.0.0/24 --gateway=10.10.0.254 dev-bridge
```


Start env
=========
Little utility script

```bash
 # starts yo/name images in a container
 $ dockit name

 # build yo/name images
 $ dockit -b name

 # stop the container name
 $ dockit -s name
```
