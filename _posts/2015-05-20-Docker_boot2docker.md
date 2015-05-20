---
layout: post
title: Docker Note - 001 boot2docker
category: ops
tag: [ops,boot2docker,docker,linux,osx,cloud,artifact delivery]
shortinfo: set up docker env in osx by boot2docker
---

Docker Note - 001 boot2docker

#boot2docker

##startup/shutdown boot2docker
```
[iflexajax@zeta:~ ]$ boot2docker up
Waiting for VM and Docker daemon to start...
................ooo
Started.
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/ca.pem
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/cert.pem
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/key.pem
Your environment variables are already set correctly.


[iflexajax@zeta:~ ]$ boot2docker down

```

## Socker / IP
```
[iflexajax@zeta:~ ]$ boot2docker socket
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/ca.pem
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/cert.pem
Writing /Users/iflexajax/.boot2docker/certs/boot2docker-vm/key.pem
    export DOCKER_HOST=tcp://192.168.59.103:2376
    export DOCKER_CERT_PATH=/Users/iflexajax/.boot2docker/certs/boot2docker-vm
    export DOCKER_TLS_VERIFY=1
[iflexajax@zeta:~ ]$ boot2docker ip
192.168.59.103
```
