# fangtian

```bash
LD_LIBRARY_PATH=/data1/zengzw/apps/miniconda3/envs/yolov5/lib \
python train.py \
--weights yolov5s.pt \
--cfg yolov5s.yaml \
--data fangtian.yaml \
--epochs 100 \
--batch-size 24 \
--imgsz 1280 \
--device 2,3 \
--project ../../experiments/fangtian \
--name baseline \
--cos-lr \
--patience 200 \
--seed 8888
```
