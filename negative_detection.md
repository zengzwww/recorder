# negative_detection

## Build

```bash
OPENCV_DIR=$(pwd)/../../3rdparty/opencv/amd64 TORCH_DIR=$(pwd)/../../3rdparty/libtorch/amd64/libtorch INFERENCE_DIR=$(pwd)/../../3rdparty/inference SPDLOG_DIR=$(pwd)/../../3rdparty/spdlog_header JSON_DIR=$(pwd)/../../3rdparty/json_header ZMQ_DIR=$(pwd)/../../3rdparty/libzmq cmake ../nd_lib/
```

## Make tag

```bash
git checkout d01e7e6f
GIT_COMMITTER_DATE="$(git show --format=%aD | head -1)" git tag -a v1.3.0 -m "v1.3.0"
git push origin --tags
```
