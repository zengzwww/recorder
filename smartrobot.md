```bash
conda create -n smartrobot python=3.8  
conda activate smartrobot  
conda remove -n smartrobot --all
```

```bash
pip download -r ../modelbuilder/requirements.txt  
pip download -r ../modeldeployer/requirements.txt  
pip install numpy==1.19.5 --find-links deps/ --no-index 
pip install -r requirements.txt --find-links deps/ --no-index 
```

```bash
sudo apt-get install libxcb-xinerama0  
pip install labelImg --find-links datamanager/labelImg/ --no-index  
```

```bash
sudo apt-get install libxslt1-dev zlib1g zlib1g-dev libglib2.0-0 \
libsm6 libgl1-mesa-glx libprotobuf-dev gcc  
pip install modeldeployer/rknn-toolkit2/rknn_toolkit2-1.4.0_22dcfef4-cp38-cp38-linux_x86_64.whl  
```
