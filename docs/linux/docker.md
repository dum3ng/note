# docker

<!-- TOC -->autoauto- [docker](#docker)auto  - [command](#command)auto    - [get all stopped container](#get-all-stopped-container)auto    - [remove all stopped container](#remove-all-stopped-container)auto    - [COPY](#copy)auto  - [network](#network)auto    - [single host network communication](#single-host-network-communication)auto      - [bridge](#bridge)auto      - [host](#host)auto      - [container](#container)auto      - [none](#none)autoauto<!-- /TOC -->

## command

### get all stopped container

```bash
docker ps --filter "status=exited" -q
```

### remove all stopped container

```bash
docker rm $(docker ps --filter "status=exited" -q)
```

### COPY

```Dockerfile
COPY  folder/*  /usr/app/folder
```

note that the above command will reduce a file hierarcy level to destination folder.

## network

### single host network communication

`docker run --network <mode>`

- bridge
- host
- container
- none

#### bridge

#### host

共享宿主机网络

#### container

共享某个 container 的网络

#### none

有自己的 network namespace， 但是没有网卡，ip，路由信息
