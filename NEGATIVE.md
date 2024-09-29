# Negative

变电站负样本缺陷识别算法库. 模型推理采用NVIDIA Triton优化.

## 环境依赖

- tritonserver: 23.10-py3
- tritonclient: 2.49.0

## ✅ 已集成的算法列表

- [x] 表计表盘属性识别
- [ ] 表计外壳属性识别
- [ ] 呼吸器硅胶桶属性识别
- [ ] 呼吸器油封属性识别

## 运行算法

### 启动模型仓库服务端

```bash
docker run -d --gpus=all -it --shm-size=256m --ipc=host --rm -p8000:8000 -p8003:8001 -p8002:8002 -v $(pwd)/model_repository:/models nvcr.io/nvidia/tritonserver:23.10-py3 /opt/tritonserver/bin/tritonserver --model-repository=/models
```

### 运行模型客户端

```bash
python tools/glass_cls_ensemble.py
```

## Triton

### 编译模型plan文件

进入triton服务端容器
```bash
docker run --privileged --gpus=all -it --shm-size=256m --ipc=host --rm -p8000:8000 -p8003:8001 -p8002:8002 -v $(pwd)/model_repository:/models nvcr.io/nvidia/tritonserver:23.10-py3
```

生成模型的plan文件, 重点优化单张图片推理, 最大支持批次推理大小为8. 以表计表盘属性识别为例(事先将glass_cls.onnx置于[存放模型文件的目录](model_repository/glass_cls/1)下)
```bash
/usr/src/tensorrt/bin/trtexec --onnx=/models/glass_cls/1/glass_cls.onnx --saveEngine=/models/glass_cls/1/model.plan --minShapes=input:1x3x224x224 --optShapes=input:1x3x224x224 --maxShapes=input:8x3x224x224
```

### 性能优化

#### 性能分析工具

安装triton sdk
```bash
export RELEASE=23.10
docker pull nvcr.io/nvidia/tritonserver:${RELEASE}-py3-sdk
docker run --gpus all --rm -it --net host nvcr.io/nvidia/tritonserver:${RELEASE}-py3-sdk
```

运行perf_analyzer
```bash
perf_analyzer -m glass_ml_cls --percentile=95 --concurrency-range 1:8 --shape input:1,3,224,224
```

#### 性能优化

两条基本的优化规则
- 最小延迟: 并发量=1, 禁用动态批次, 模型实例数=1
- 最大吞吐量: $ 并发量=2\times 最大批次大小\times 模型实例数 $

## FAQ
### OSError: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.34' not found
启动triton客户端报如下错误
```text
Traceback (most recent call last):
  File "/mnt/data/xxx/codes/meter/tests/triton.py", line 3, in <module>
    import tritonclient.utils.shared_memory as shm
  File "/home/industai/miniconda3/envs/substation/lib/python3.9/site-packages/tritonclient/utils/shared_memory/__init__.py", line 52, in <module>
    _cshm = cdll.LoadLibrary(_cshm_path)
  File "/home/industai/miniconda3/envs/substation/lib/python3.9/ctypes/__init__.py", line 460, in LoadLibrary
    return self._dlltype(name)
  File "/home/industai/miniconda3/envs/substation/lib/python3.9/ctypes/__init__.py", line 382, in __init__
    self._handle = _dlopen(self._name, mode)
OSError: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.34' not found (required by /home/industai/miniconda3/envs/substation/lib/python3.9/site-packages/tritonclient/utils/shared_memory/libcshm.so)
```

解决办法为升级glibc
```bash
strings /lib/x86_64-linux-gnu/libc.so.6 |grep GLIBC_
```

```bash
sudo vi /etc/apt/sources.list
```

```text
deb http://th.archive.ubuntu.com/ubuntu jammy main
```

```bash
sudo apt update
sudo apt install libc6
```
