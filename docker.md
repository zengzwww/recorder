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
