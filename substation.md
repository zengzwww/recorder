# Substation

```bash
yolo detect train model=yolov8m.pt data=../../data/substation/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/dataset.yaml epochs=300 patience=300 batch=48 imgsz=960 device=1,2 project=../../experiments/ssd name=1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48 pretrained=True seed=8888 cos_lr=True degrees=30 shear=30
```

```bash
yolo detect val model=../../experiments/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/weights/best.pt data=../../data/substation/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/dataset.yaml save_txt=True save_conf=True project=../../experiments/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48 name=val
```

```bash
yolo detect predict model=../../experiments/baseline/weights/70Detect.pt source=../../data/substation/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/yolo/images/val/ conf=0.25 iou=0.7 imgsz=640 project=../../experiments/baseline/ name=pred save_txt=True save_conf=True
```

```bash
yolo detect predict model=../../experiments/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/weights/best.pt source=../../data/substation/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/yolo/images/val/ conf=0.25 iou=0.7 imgsz=960 project=../../experiments/ssd/1afb9ff1e9ce0129dd1091bbffc9cd3b5e909b48/ name=pred save_txt=True save_conf=True
```

```bash
FIFTYONE_DATABASE_URI=mongodb://127.0.0.1:27017 fiftyone datasets create --name ssd_val --dataset-dir data/substation/cabinet/coco/3.0 --type fiftyone.types.COCODetectionDataset
```
