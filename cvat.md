# cvat

## Run

[Set CVAT hostname and version](https://opencv.github.io/cvat/docs/faq/#how-to-change-default-cvat-hostname-or-port)
```bash
CVAT_HOST=10.0.0.47 CVAT_VERSION=v2.9.0 docker compose up -d
```

For remote acccess (e.g http://www.aimall-cd.cn:8035/):
```bash
CVAT_HOST=www.aimall-cd.cn CVAT_VERSION=v2.9.0 docker compose up -d
```

```bash
CVAT_HOST=172.20.40.13 CVAT_VERSION=v2.31.0 docker compose up -d
```

```text
http://172.20.40.13:8080/auth/login
```
