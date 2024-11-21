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

安装NVIDIA Container Toolkit参考[Installing the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

如果下面的命令报错
```bash
sudo apt-get install -y nvidia-container-toolkit
```

```text
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ibus-data libpinyin-data libpinyin13 python3-ibus-1.0
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libnvidia-container-tools libnvidia-container1 nvidia-container-toolkit-base
The following NEW packages will be installed:
  libnvidia-container-tools libnvidia-container1 nvidia-container-toolkit nvidia-container-toolkit-base
0 upgraded, 4 newly installed, 0 to remove and 94 not upgraded.
Need to get 4,050 kB of archives.
After this operation, 15.7 MB of additional disk space will be used.
Err:1 https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64  libnvidia-container1 1.13.5-1
  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
Err:2 https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64  libnvidia-container-tools 1.13.5-1
  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
Err:3 https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64  nvidia-container-toolkit-base 1.13.5-1
  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
Err:4 https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64  nvidia-container-toolkit 1.13.5-1
  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
E: Failed to fetch https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64/./libnvidia-container1_1.13.5-1_amd64.deb  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
E: Failed to fetch https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64/./libnvidia-container-tools_1.13.5-1_amd64.deb  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
E: Failed to fetch https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64/./nvidia-container-toolkit-base_1.13.5-1_amd64.deb  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
E: Failed to fetch https://nvidia.github.io/libnvidia-container/stable/ubuntu18.04/amd64/./nvidia-container-toolkit_1.13.5-1_amd64.deb  Could not handshake: Error in the pull function. [IP: 2606:50c0:8002::153 443]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
```

就用
```bash
sudo -E apt-get install -y nvidia-container-toolkit
```

安装triton server, 参考[Triton Inference Server](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tritonserver)和[Triton Inference Server Release 23.10](https://docs.nvidia.com/deeplearning/triton-inference-server/release-notes/rel-23-10.html#rel-23-10)
