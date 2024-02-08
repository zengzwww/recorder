# open-mmlab

## mmpretrain

在自己的数据集上微调预训练模型
```bash
CUDA_VISIBLE_DEVICES=0 python tools/train.py ./configs/aimall/resnet18_finetune_carbinet.py --work-dir ../training_outputs/cabinet_cls_20230530.2 --auto-scale-lr
```

测试训练的模型
```bash
python tools/test.py ./configs/aimall/resnet18_finetune_carbinet.py ../training_outputs/cabinet_cls_20230529.2/epoch_30.pth --work-dir ../training_outputs/cabinet_cls_20230529.2 --show-dir ../training_outputs/cabinet_cls_20230529.2/visres
```

## mmdeploy

* 模型转换器的依赖项复用mmpretrain的
* 推理引擎(ONNX)

安装Python包
```bash
pip install onnxruntime==1.8.1
```
安装预编译二进制包
```bash
wget https://github.com/microsoft/onnxruntime/releases/download/v1.8.1/onnxruntime-linux-x64-1.8.1.tgz
tar -zxvf onnxruntime-linux-x64-1.8.1.tgz
cd onnxruntime-linux-x64-1.8.1
export ONNXRUNTIME_DIR=$(pwd)
export LD_LIBRARY_PATH=$ONNXRUNTIME_DIR/lib:$LD_LIBRARY_PATH
```

* 编译mmdeploy
```bash
cd /the/root/path/of/MMDeploy
export MMDEPLOY_DIR=$(pwd)
```
编译ONNX的Ops
```bash
cd ${MMDEPLOY_DIR}
mkdir -p build && cd build
cmake -DCMAKE_CXX_COMPILER=g++-7 -DMMDEPLOY_TARGET_BACKENDS=ort -DONNXRUNTIME_DIR=${ONNXRUNTIME_DIR} ..
make -j$(nproc) && make install
```
安装模型转换器
```bash
cd ${MMDEPLOY_DIR}
mim install -e .
```

* 导出ONNX模型(分类)
```bash
python tools/torch2onnx.py configs/mmpretrain/classification_onnxruntime_static.py ../mmpretrain/configs/aimall/resnet18_finetune_carbinet.py ../training_outputs/cabinet_cls_20230529.2/epoch_30.pth ../data/cabinet_cls/前柜_紫菱服务/0d5fe4346a67c04f1a28c1db33042b14_0.jpg --work-dir ../training_outputs/cabinet_cls_20230529.2
```
