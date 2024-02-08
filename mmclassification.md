# 在mmclassification框架下训练图像分类器

## 安装基础依赖项

```
cd ~/workspace/downloads
sh Miniconda3-py37_23.1.0-1-Linux-x86_64.sh
conda create -n open-mmlab python=3.7
conda activate open-mmlab
pip install torch-1.8.0+cu111-cp37-cp37m-linux_x86_64.whl
pip install torchvision-0.9.0+cu111-cp37-cp37m-linux_x86_64.whl
pip install tensorboard
```

## 安装mmclassification

```
pip3 install openmim
mim install mmcv-full
git clone https://github.com/open-mmlab/mmclassification.git
cd mmclassification
pip3 install -e .
```

## 准备数据集


## 训练

python tools/train.py ${CONFIG_FILE} [optional arguments]  
python tools/train.py price_sticker_20230321a.py --work_dir ~/workspace/exps/price_sticker_20230321a  

./tools/dist_train.sh ${CONFIG_FILE} ${GPU_NUM} [optional arguments]  
./tools/dist_train.sh price_sticker_20230321a.py 4 --work_dir ~/workspace/exps/price_sticker_20230321a  

## 发布模型

python tools/convert_models/publish_model.py ${INPUT_FILENAME} ${OUTPUT_FILENAME}  
python tools/convert_models/publish_model.py work_dirs/resnet50/latest.pth imagenet_resnet50.pth  
