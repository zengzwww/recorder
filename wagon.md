# wagon

## 安装

```bash
rm -r /tmp/wagon
mkdir -p /tmp/wagon
tar -xvf ~/下载/wagon_linux_amd64.tar.gz -C /tmp/wagon
sh ../tmp/wagon_install.sh
```

## 本地编译

```bash
export GOPROXY=https://goproxy.cn,direct
export GOPRIVATE=git.innoai.tech
export GONOSUMDB=git.innoai.tech
export DAGGER_LOG_FORMAT=plain
export CONTAINER_REGISTRY_PASSWORD=LUSI1CkYKVpl9K6zvOxb35Z4CyTsymRk
export CONTAINER_REGISTRY_USERNAME=zengzhiwei
export BUILDKIT_HOST=tcp://172.25.1.28:32231
export LINUX_MIRROR=http://repo.huaweicloud.com
```

```bash
wagon get -u ./...
wagon do
wagon do build_amd64
```

## 查看镜像中的文件

- 将镜像报错为本地文件
```bash
docker save -o image.tar harbor.innoai.tech/ai/electric-power/negative_detection:dev-CUDA-9428b9fd-amd64
```

- 解压image.tar到image
- 解压image/blobs/sha256/8f588381b45cb4831e2885a27a8e38097e0169171851bad29c5447a05fe81574，即可在image/blobs/sha256/8f588381b45cb4831e2885a27a8e38097e0169171851bad29c5447a05fe81574目录下看到库文件
