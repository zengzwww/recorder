# Face algorithms

| 模型 | 作用 | 大小 | 可否量化
| :-: | :-: | :-: | :-:
| [2d106det.onnx](https://github.com/deepinsight/insightface/blob/master/alignment/coordinate_reg/README.md) | 提取106个2D关键点 | 5MB |
| [fcn8s_500.onnx](https://github.com/YuvalNirkin/face_segmentation) | 人脸分割 | 538MB | YES
| fd_2.0.1.onnx | 人脸检测 | 8.2MB |
| fiqa_1.0.onnx | 人脸质量 | 0.8MB |
| flm_0.1.onnx | 人脸关键点 | 1.6MB |
| genderage.onnx |  | 1.3MB |
| [GFPGANv1.4.onnx](https://github.com/TencentARC/GFPGAN) | 人脸复原 | 341.7MB |NO
| [inswapper_128.onnx](https://github.com/haofanwang/inswapper) | 换脸 | 554.3MB |
| [w600k_r50.onnx](https://github.com/deepinsight/insightface/tree/master/python-package) | 人脸特征提取 | 174.4MB | YES

| 2d106det.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x192x192
| 推理 | 1x212

| fcn8s_500.onnx | 输出大小
| :-: | :-:
| 输入 | 192x192x3
| 预处理 | 1x500x500x3
| 推理 | 1x500x500x21
| 后处理 | 192x192

| fd_2.0.1.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x512x512
| 推理 | 1x2x128x128, 1x2x128x128, 1x2x128x128, 1x10x128x128
| 后处理 | Nx15

| fiqa_1.0.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x48x48
| 推理 | 1x1

| flm_0.1.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x48x48
| 推理 | 1x2, 1x4, 1x10

| GFPGANv1.4.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x512x512
| 推理 | 1x3x512x512

| inswapper_128.onnx | 输出大小
| :-: | :-:
| 预处理 | 1x3x128x128, 1x512
| 推理 | 1x3x128x128

| w600k_r50.onnx | 输出大小
| :-: | :-:
| 输入 | ?x?x3
| 预处理 | 1x3x112x112
| 推理 | 1x512

## Triton deploy

各个版本的Trition及driver
https://docs.nvidia.com/deeplearning/triton-inference-server/release-notes/rel-22-10.html

```bash
service docker start
systemctl start docker
service docker stop
systemctl stop docker
```

更改模型输入大小[参考](https://onnxruntime.ai/docs/tutorials/mobile/helpers/make-dynamic-shape-fixed.html)
```bash
python -m onnxruntime.tools.make_dynamic_shape_fixed --input_name input0 --input_shape 1,3,512,512 model_repository/fd_2.0.1.onnx model_repository/fd_2.0.1_fix.onnx
```

```bash
cd faceswap_triton
cd model_repository
mkdir -p 2d106det/1 fcn8s_500/1 fd_2.0.1/1 fiqa_1.0/1 flm_0.1/1 w600k_r50/1
cd ..
sudo docker run --gpus=all -it --shm-size=256m --rm -p8000:8000 -p8001:8001 -p8002:8002 -v $(pwd)/model_repository:/models nvcr.io/nvidia/tritonserver:23.10-py3
sudo docker run --gpus=all -it --shm-size=256m --ipc=host --rm -p8000:8000 -p8001:8001 -p8002:8002 -v $(pwd)/model_repository:/models nvcr.io/nvidia/tritonserver:23.10-py3
```

```bash
/usr/src/tensorrt/bin/trtexec --onnx=/models/2d106det.onnx --saveEngine=/models/2d106det/1/model.plan --fp16
/usr/src/tensorrt/bin/trtexec --onnx=/models/fcn8s_500.onnx --saveEngine=/models/fcn8s_500/1/model.plan --fp16
/usr/src/tensorrt/bin/trtexec --onnx=/models/fd_2.0.1_fix.onnx --saveEngine=/models/fd_2.0.1/1/model.plan --fp16
/usr/src/tensorrt/bin/trtexec --onnx=/models/fiqa_1.0.onnx --saveEngine=/models/fiqa_1.0/1/model.plan --fp16
/usr/src/tensorrt/bin/trtexec --onnx=/models/flm_0.1.onnx --saveEngine=/models/flm_0.1/1/model.plan --fp16
/usr/src/tensorrt/bin/trtexec --onnx=/models/w600k_r50.onnx --saveEngine=/models/w600k_r50/1/model.plan --fp16
```

```bash
pip3 install opencv-python-headless -i https://mirrors.aliyun.com/pypi/simple/
tritonserver --model-repository=/models
```

保存镜像文件
```bash
sudo docker commit 49adccc602bb nvcr.io/nvidia/tritonserver:23.10-py3-face
sudo docker save -o tritonserver.tar nvcr.io/nvidia/tritonserver:23.10-py3-face
```

[保存的时候压缩一下](https://phoenixnap.com/kb/docker-export)
```bash
docker export 5c36fcb468ef | gzip > tritonserver.tar.gz
```

```bash
pip install tritonclient[all]
pip install tritonclient\[all\]

```

```bash
perf_analyzer -m fd_2.0.1 -b 1 --shared-memory system --output-shared-memory-size 655360 --shape input0:1,3,512,512 --concurrency-range 2:16:2 --percentile=95
```


```bash
perf_analyzer -m face_ensemble -b 1 --shape images:1,1080,1920,3 --concurrency-range 2:16:2 --percentile=95
perf_analyzer -m face_ensemble -a -b 1 --shape images:1,1080,1920,3 --concurrency-range 2:16:2 --percentile=95
perf_analyzer -m face_ensemble -a -b 1 --shared-memory system --shape images:1,1080,1920,3 --concurrency-range 2:16:2 --percentile=95
```

[threadpoolexecutor-pipeline](https://superfastpython.com/threadpoolexecutor-pipeline/)
