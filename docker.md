# Docker

## How to change docker root data directory

see [here](https://tienbm90.medium.com/how-to-change-docker-root-data-directory-89a39be1a70b)

## How to set proxy

```bash
mkdir -p /etc/systemd/system/docker.service.d
vim /etc/systemd/system/docker.service.d/http-proxy.conf
```

Add next:

```text
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:8001"
Environment="HTTPS_PROXY=http://127.0.0.1:8001"
```

```bash
systemctl daemon-reload
systemctl restart docker
systemctl show --property=Environment docker
```

see [here](https://linux.do/t/topic/111276)

## Install docker in Ubuntu20.04

参考链接: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

执行第一步就报错

```bash
sudo apt-get update
```

```text
Could not handshake: Error in the pull function. [IP: 185.199.111.153 443]
```

解决办法参考: [Unable to install nvidia-docker on Ubuntu 18.04](https://github.com/NVIDIA/nvidia-docker/issues/1296)

```bash
sudo -E apt-get update
```
