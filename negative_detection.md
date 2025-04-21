# negative_detection

## Build

```bash
OPENCV_DIR=$(pwd)/../../3rdparty/opencv/amd64 TORCH_DIR=$(pwd)/../../3rdparty/libtorch/amd64/libtorch INFERENCE_DIR=$(pwd)/../../3rdparty/inference SPDLOG_DIR=$(pwd)/../../3rdparty/spdlog_header JSON_DIR=$(pwd)/../../3rdparty/json_header ZMQ_DIR=$(pwd)/../../3rdparty/libzmq cmake ../nd_lib/
```

```bash
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection srv-ai-adapter--gpu-848b887759-hlc8k:/home
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/3rdparty/json_header/ srv-ai-adapter--gpu-848b887759-hlc8k:/home
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/3rdparty/spdlog_header/ srv-ai-adapter--gpu-848b887759-hlc8k:/home

OPENCV_DIR=/usr/local/pkg/opencv/amd64 TORCH_DIR=/usr/local/pkg/libtorch/amd64/libtorch INFERENCE_DIR=/usr/local/pkg/inference/amd64 ZMQ_DIR=/usr/local/pkg/libzmq/amd64 SPDLOG_DIR=$(pwd)/../../spdlog_header JSON_DIR=$(pwd)/../../json_header cmake ../nd_lib/

kubectl -n sentry cp /home/industai/zengzw/codes/data/nc srv-ai-adapter--gpu-848b887759-hlc8k:/home
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models/ srv-ai-adapter--gpu-848b887759-hlc8k:/home

LD_LIBRARY_PATH=$(pwd)/../lib:$LD_LIBRARY_PATH ../bin/nd_demo --img_dir=/home/meter2 --save_dir=/home/meter2_nd/
```

```bash
sshfs industai@172.20.40.46:/mnt/data/zengzw/codes/innoai /home/industai/zengzw/codes/
kubectl -n sentry cp /home/industai/zengzw/codes/negative_detection srv-ai-adapter--gpu-68566d7f4c-9ptpp:/home
kubectl -n sentry cp /home/industai/zengzw/codes/3rdparty/json_header/ srv-ai-adapter--gpu-68566d7f4c-9ptpp:/home
kubectl -n sentry cp /home/industai/zengzw/codes/3rdparty/spdlog_header/ srv-ai-adapter--gpu-68566d7f4c-9ptpp:/home
kubectl -n sentry cp /home/industai/zengzw/codes/data srv-ai-adapter--gpu-68566d7f4c-9ptpp:/home
kubectl -n sentry cp /home/industai/zengzw/codes/models/ srv-ai-adapter--gpu-68566d7f4c-9ptpp:/home
LD_LIBRARY_PATH=$(pwd)/../lib:$LD_LIBRARY_PATH ../bin/nd_demo --img_dir=/home/meter2 --save_dir=/home/meter2_nd/
```

## Make tag

```bash
git checkout d01e7e6f
GIT_COMMITTER_DATE="$(git show --format=%aD | head -1)" git tag -a v1.3.0 -m "v1.3.0"
git push origin --tags
```
