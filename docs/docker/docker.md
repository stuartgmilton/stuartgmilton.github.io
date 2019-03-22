---
layout: default
title: Docker
nav_order: 4
has_children: true
permalink: /docs/docker
---

# Docker

```
sudo yum install -y \
  yum-utils \
  device-mapper-persistent-data \
  lvm2
```
```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
```
sudo yum install -y \
  docker-ce \
  docker-ce-cli \
  containerd.io
```

Run your first docker container
```
sudo docker run hello-world
```

Doh, it won’t work…

sudo mkdir /etc/systemd/system/docker.service.d
sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf

Paste the below in;

[Service]
Environment="HTTP_PROXY=http://127.0.0.1:3128/"
Environment="HTTPS_PROXY=http://127.0.0.1:3128/"

Flush these changes by running:
sudo systemctl daemon-reload


Verify that the configuration has been loaded:
sudo systemctl show --property Environment docker
Environment=HTTP_PROXY=http://127.0.0.1:3128/ HTTPS_PROXY=http://127.0.0.1:3128/


Restart Docker
sudo systemctl restart docker

Run your first docker container
sudo docker run hello-world

View all downloaded container images
sudo docker images

View all running containers
sudo docker ps

Get docker to start on boot:
sudo systemctl enable docker
{:toc}
