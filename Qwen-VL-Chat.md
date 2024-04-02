# Qwen-VL-Chat

### Docker


```bash
docker pull pytorch/pytorch:2.2.1-cuda12.1-cudnn8-runtime
docker run --gpus all -v ${PWD}:/workspace/lvm --rm -it --entrypoint /bin/bash pytorch/pytorch:2.2.1-cuda12.1-cudnn8-runtime
```

#### 编译镜像

```bash
docker build -t lvm:0.1.0 --platform linux/amd64 -f Dockerfile . 
```

#### 运行镜像

```bash
docker run -it --gpus all -d --restart always -v ${PWD}:/var/app --name lvm -p 8086:8086 --user=20001:20001 --platform linux/amd64 lvm:0.1.0
```
