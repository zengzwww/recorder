# RK-YOLOv5

## Installation

```bash
git clone https://github.com/airockchip/yolov5.git
cd yolov5
conda create -n rk-yolov5 python=3.7
conda activate rk-yolov5
pip install -r requirements.txt
```

## Detect objects

```
python detect.py --weights ../../model_zoo/yolov5/yolov5s.onnx --source data/images/bus.jpg --data data/coco.yaml --imgsz 640 --device cpu --half
```

## Training

```bash
python train.py --img-size 640 --batch-size 64 --epochs 3 --data coco128_my.yaml --weights ../../model_zoo/yolov5/yolov5s.pt
```
