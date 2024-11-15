# imgrec_server

图像识别服务端.

## Docker封装

- 准备Dockerfile文件
```text
FROM harbor.innoai.tech/c3rd/python-cuda-runtime:feature-cuda11.7-python3.11-torch2.0.1-20.04-1.0.0-6e3093cf-amd64

WORKDIR /usr/src/app

COPY . /usr/src/imgrec_server

RUN cp /usr/src/imgrec_server/tools/run.sh /usr/src/app && \
    chmod +x /usr/src/app/run.sh && \
    pip install flask -i https://mirrors.aliyun.com/pypi/simple

EXPOSE 5000

ENTRYPOINT ["/usr/src/app/run.sh"]

CMD ["--host", "0.0.0.0", "--port", "5000"]
```

- 编译Docker镜像
- 
```bash
docker build -t industai:v1.0 .
```

- 启动服务端容器

```bash
docker run -it --privileged --gpus=all --shm-size=256m --ipc=host --rm -p5000:5000 industai:v1.0
```

也可指定host和port
```bash
docker run -it --privileged --gpus=all --shm-size=256m --ipc=host --rm -p5000:5000 industai:v1.0 --port 5000
```

如果想绕过默认的入口，可执行
```bash
docker run -it --privileged --gpus=all --shm-size=256m --ipc=host --rm -p5000:5000 --entrypoint bash industai:v1.0
```

- 保存镜像

```bash
docker save -o industai-1.0.tar industai:v1.0
```
