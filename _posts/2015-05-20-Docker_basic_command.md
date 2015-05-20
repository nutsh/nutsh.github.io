---
layout: post
title: Docker Note - 002 basic commands
category: ops
tag: [ops,docker,linux,cloud,artifact delivery]
shortinfo: docker run [-i] [-t] [-p] [-d] , docker ps [-a] [-q] , docker rm , docker start/stop, docker alias , docker logs , docker port,diff,cp,inspect
---

Docker Note - 002 commands


#docker concept

- docker container
- docker Images (saved status of container)
- docker files (Series of commands to build an images)

- docker Engine
- Docker hub


# docker commands

##docker run
```
[iflexajax@zeta:~ ]$ docker run busybox echo 'hello world'
Unable to find image 'busybox:latest' locally
511136ea3c5a: Pull complete
df7546f9f060: Pull complete
ea13149945cb: Pull complete
4986bf8c1536: Pull complete
busybox:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
Status: Downloaded newer image for busybox:latest
hello world
```

##docker run (-i --interactive -t --tty)

```
[iflexajax@zeta:~ ]$ docker run -it ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
f3c84ac3a053: Pull complete
f3c84ac3a053: Download complete
a1a958a24818: Download complete
9fec74352904: Download complete
d0955f21bf24: Download complete
511136ea3c5a: Download complete
Status: Downloaded newer image for ubuntu:latest
root@e6a20a8d3bfc:/#
```


##docker run (-p port)

```
[iflexajax@zeta:~ ]$ docker run  -p 8000:80 atbaker/nginx-example
The nginx server is running
```

```
curl http://192.168.59.103:8000/
```

```
192.168.59.3 - - [08/Apr/2015:06:30:58 +0000] "GET / HTTP/1.1" 200 14974 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.118 Safari/537.36" "-"
2015/04/08 06:30:58 [error] 6#0: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 192.168.59.3, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "192.168.59.103:8000"
192.168.59.3 - - [08/Apr/2015:06:30:58 +0000] "GET /favicon.ico HTTP/1.1" 404 571 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.118 Safari/537.36" "-"
```

##docker run (-d detach)
```
[iflexajax@zeta:~ ]$ docker run -d -p 8000:80 atbaker/nginx-example
cd8b508d9207f9ef1289c6fe5bc56f83c4cbca06397f94ff0c4d96d63435e648
```

##docker ps
```
[iflexajax@zeta:~ ]$ docker ps
CONTAINER ID        IMAGE                          COMMAND                CREATED             STATUS              PORTS                           NAMES
e238cccc4659        atbaker/nginx-example:latest   "/command_wrapper.sh   20 seconds ago      Up 18 seconds       443/tcp, 0.0.0.0:8000->80/tcp   berserk_mestorf

#all
[iflexajax@zeta:~ ]$ docker ps -a
CONTAINER ID        IMAGE                          COMMAND                CREATED             STATUS                         PORTS               NAMES
a3e232ed7ed1        atbaker/nginx-example:latest   "/command_wrapper.sh   57 minutes ago      Exited (0) 9 minutes ago                           stoic_stallman
e6a20a8d3bfc        ubuntu:14.04                   "/bin/bash"            About an hour ago   Exited (0) About an hour ago                       focused_feynman
260d586351e5        busybox:latest                 "ping google.com"      3 hours ago         Exited (1) 3 hours ago                             clever_brattain
73a1f4fcd1b2        busybox:latest                 "echo 'Hello Ajax'"    3 hours ago         Exited (0) 3 hours ago                             naughty_yonath
d94fe18daa04        nutsh/redis-password:latest    "redis-server /usr/s   6 weeks ago         Exited (0) 5 weeks ago                             thirsty_hawking
7f3f0fa3b0c7        atbaker/redis-example:latest   "/bin/bash"            6 weeks ago         Exited (0) 6 weeks ago                             elated_jang
15b3e48246f1        postgres:latest                "/docker-entrypoint.   6 weeks ago         Exited (0) 6 weeks ago                             cranky_goodall


# Only display numeric IDs
[iflexajax@zeta:~ ]$ docker ps -a -q
29526b973521
a3e232ed7ed1
e6a20a8d3bfc
260d586351e5
73a1f4fcd1b2
d94fe18daa04
7f3f0fa3b0c7
15b3e48246f1

# rm all
[iflexajax@zeta:~ ]$ docker rm -f $(docker ps -aq)
29526b973521
a3e232ed7ed1
e6a20a8d3bfc
260d586351e5
73a1f4fcd1b2
d94fe18daa04
7f3f0fa3b0c7
15b3e48246f1

```

##docker stop/start

```
[iflexajax@zeta:~ ]$ docker stop e238
e238
[iflexajax@zeta:~ ]$ docker start e238
e238
```

##docker rm

```
[iflexajax@zeta:~ ]$ docker rm -f e238
e238
[iflexajax@zeta:~ ]$ docker start e238
e238
```

##docker name

```
[iflexajax@zeta:~ ]$ docker run -d -p 8000:80 --name webserver atbaker/nginx-example
29526b9735211b404572dd3aaa2eb35a97f100214293900752640062bbdd9fec

[iflexajax@zeta:~ ]$ docker ps
CONTAINER ID        IMAGE                          COMMAND                CREATED             STATUS              PORTS                           NAMES
29526b973521        atbaker/nginx-example:latest   "/command_wrapper.sh   13 seconds ago      Up 12 seconds       443/tcp, 0.0.0.0:8000->80/tcp   webserver


[iflexajax@zeta:~ ]$ docker stop webserver
webserver

[iflexajax@zeta:~ ]$ docker start webserver
webserver


[iflexajax@zeta:~ ]$ docker attach webserver
192.168.59.3 - - [20/May/2015:11:13:20 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
192.168.59.3 - - [20/May/2015:11:13:22 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
```

##docker logs

```
[iflexajax@zeta:~ ]$ docker logs webserver
The nginx server is running
192.168.59.3 - - [20/May/2015:11:05:17 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"

[iflexajax@zeta:~ ]$ docker logs -f  webserver
The nginx server is running
192.168.59.3 - - [20/May/2015:11:05:17 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
192.168.59.3 - - [20/May/2015:11:09:21 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
192.168.59.3 - - [20/May/2015:11:09:23 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"


[iflexajax@zeta:~ ]$ docker logs -f -t  webserver
2015-05-20T11:04:34.389204043Z The nginx server is running
2015-05-20T11:05:17.972960399Z 192.168.59.3 - - [20/May/2015:11:05:17 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
2015-05-20T11:09:21.429912576Z 192.168.59.3 - - [20/May/2015:11:09:21 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
2015-05-20T11:09:23.154134503Z 192.168.59.3 - - [20/May/2015:11:09:23 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2406.0 Safari/537.36" "-"
```


##docker port
```
[iflexajax@zeta:~ ]$ docker start webserver
webserver
[iflexajax@zeta:~ ]$ docker port webserver 80
0.0.0.0:8000
```

##docker diff
```
[iflexajax@zeta:~ ]$ docker diff webserver
C /run
A /run/nginx.pid
```

##docker cp
```
[iflexajax@zeta:~ ]$ docker cp  --help

Usage: docker cp [OPTIONS] CONTAINER:PATH HOSTPATH

Copy files/folders from the PATH to the HOSTPATH

  --help=false       Print usage

```

##docker inspect
```
[iflexajax@zeta:~ ]$ docker inspect --help

Usage: docker inspect [OPTIONS] CONTAINER|IMAGE [CONTAINER|IMAGE...]

Return low-level information on a container or image

  -f, --format=""    Format the output using the given go template.
  --help=false       Print usage


  [iflexajax@zeta:~ ]$ docker inspect --help

  Usage: docker inspect [OPTIONS] CONTAINER|IMAGE [CONTAINER|IMAGE...]

  Return low-level information on a container or image

    -f, --format=""    Format the output using the given go template.
    --help=false       Print usage
  [iflexajax@zeta:~ ]$ docker inspect webserver
  [{
      "AppArmorProfile": "",
      "Args": [],
      "Config": {
          "AttachStderr": false,
          "AttachStdin": false,
          "AttachStdout": false,
          "Cmd": [
              "/command_wrapper.sh"
          ],
          "CpuShares": 0,
          "Cpuset": "",
          "Domainname": "",
          "Entrypoint": null,
          "Env": [
              "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
              "NGINX_VERSION=1.7.11-1~wheezy"
          ],
          "ExposedPorts": {
              "443/tcp": {},
              "80/tcp": {}
          },
          "Hostname": "29526b973521",
          "Image": "atbaker/nginx-example",
          "MacAddress": "",
          "Memory": 0,
          "MemorySwap": 0,
          "NetworkDisabled": false,
          "OnBuild": null,
          "OpenStdin": false,
          "PortSpecs": null,
          "StdinOnce": false,
          "Tty": false,
          "User": "",
          "Volumes": {
              "/var/cache/nginx": {}
          },
          "WorkingDir": ""
      },
      "Created": "2015-05-20T11:04:34.023200789Z",
      "Driver": "aufs",
      "ExecDriver": "native-0.2",
      "ExecIDs": null,
      "HostConfig": {
          "Binds": null,
          "CapAdd": null,
          "CapDrop": null,
          "ContainerIDFile": "",
          "Devices": [],
          "Dns": null,
          "DnsSearch": null,
          "ExtraHosts": null,
          "IpcMode": "",
          "Links": null,
          "LxcConf": [],
          "NetworkMode": "bridge",
          "PidMode": "",
          "PortBindings": {
              "80/tcp": [
                  {
                      "HostIp": "",
                      "HostPort": "8000"
                  }
              ]
          },
          "Privileged": false,
          "PublishAllPorts": false,
          "ReadonlyRootfs": false,
          "RestartPolicy": {
              "MaximumRetryCount": 0,
              "Name": ""
          },
          "SecurityOpt": null,
          "VolumesFrom": null
      },
      "HostnamePath": "/mnt/sda1/var/lib/docker/containers/29526b9735211b404572dd3aaa2eb35a97f100214293900752640062bbdd9fec/hostname",
      "HostsPath": "/mnt/sda1/var/lib/docker/containers/29526b9735211b404572dd3aaa2eb35a97f100214293900752640062bbdd9fec/hosts",
      "Id": "29526b9735211b404572dd3aaa2eb35a97f100214293900752640062bbdd9fec",
      "Image": "255baa10c887333f08a140c57a2a414d0a777dca3d28a52334f853bcb7128859",
      "MountLabel": "",
      "Name": "/webserver",
      "NetworkSettings": {
          "Bridge": "docker0",
          "Gateway": "172.17.42.1",
          "GlobalIPv6Address": "",
          "GlobalIPv6PrefixLen": 0,
          "IPAddress": "172.17.0.10",
          "IPPrefixLen": 16,
          "IPv6Gateway": "",
          "LinkLocalIPv6Address": "fe80::42:acff:fe11:a",
          "LinkLocalIPv6PrefixLen": 64,
          "MacAddress": "02:42:ac:11:00:0a",
          "PortMapping": null,
          "Ports": {
              "443/tcp": null,
              "80/tcp": [
                  {
                      "HostIp": "0.0.0.0",
                      "HostPort": "8000"
                  }
              ]
          }
      },
      "Path": "/command_wrapper.sh",
      "ProcessLabel": "",
      "ResolvConfPath": "/mnt/sda1/var/lib/docker/containers/29526b9735211b404572dd3aaa2eb35a97f100214293900752640062bbdd9fec/resolv.conf",
      "RestartCount": 0,
      "State": {
          "Error": "",
          "ExitCode": 0,
          "FinishedAt": "2015-05-20T11:14:27.895925058Z",
          "OOMKilled": false,
          "Paused": false,
          "Pid": 2649,
          "Restarting": false,
          "Running": true,
          "StartedAt": "2015-05-20T11:15:21.135034064Z"
      },
      "Volumes": {
          "/var/cache/nginx": "/mnt/sda1/var/lib/docker/vfs/dir/40f17fdb0251726b084921a16562543d9b765a83beaafdbe9082b1c503740983"
      },
      "VolumesRW": {
          "/var/cache/nginx": true
      }
  }
  ]
```
