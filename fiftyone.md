# fiftyone

## 安装

```bash
all_proxy="socks5://127.0.0.1:1081" pip install fiftyone
```

## 配置

1. 安装[mongodb](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/)
```bash
sudo apt-get install gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

2. [修改权限](https://stackoverflow.com/questions/60309575/mongodb-service-failed-with-result-exit-code)
```bash
sudo chown mongodb:mongodb /tmp/mongodb-27017.sock
```

3. 启动mongodb
```bash
sudo systemctl start mongod
```

默认用户名：mongodb，默认端口：27017，fiftyone配置mongodb参考[这里](https://docs.voxel51.com/user_guide/config.html)

## 格式转换

1. YOLOv5 to COCO
```bash
FIFTYONE_DATABASE_URI=mongodb://127.0.0.1:27017 fiftyone convert --input-dir data/substation/cabinet/yolo/3.0 --input-type fiftyone.types.YOLOv5Dataset --output-dir data/substation/cabinet/coco/3.0 --output-type fiftyone.types.COCODetectionDataset --input-kwargs split=val --output-kwargs split=val
```

## 创建数据集

```bash
FIFTYONE_DATABASE_URI=mongodb://127.0.0.1:27017 fiftyone datasets create --name cabinet --dataset-dir data/substation/cabinet/coco/3.0 --type fiftyone.types.COCODetectionDataset
```

## 可视化数据集

```bash
FIFTYONE_DATABASE_URI=mongodb://127.0.0.1:27017 fiftyone app launch cabinet
```
