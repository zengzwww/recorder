# cabinet

## train

```bash
yolo detect train model=yolov8m.pt data=ultralytics/cfg/datasets/cabinet.yaml epochs=300 patience=300 batch=64 imgsz=640 device=0,1 project=../../experiments/cabinet_det name=m640 pretrained=True seed=8888 cos_lr=True degrees=30 shear=30
```

## detect

```bash
yolo detect predict model=../../experiments/cabinet_det/m640/weights/best.pt source=../../data/substation/cabinet/yolo/cabinet/images/val/ conf=0.25 iou=0.7 imgsz=640 project=../../experiments/cabinet_det/ name=predict save_txt=True
```
