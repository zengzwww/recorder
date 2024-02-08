# OpenCV

## Ubuntu系统下安装OpenCV的依赖项
参考文档OpenCV-Python Tutorials->Introduction to OpenCV->Install OpenCV-Python in Ubuntu  

## imdecode解码出来的图像异常旋转90度
使用imdecode时设置flags为IMREAD_UNCHANGED，导致解码出来的图像错误旋转了90度，这是opencv的一个bug。此时用IMREAD_COLOR标志解决这个问题。参考[stackoverflow](https://stackoverflow.com/questions/58985183/opencv-imwrite-image-get-rotated)。

## 编译opencv-contrib-python
```bash
pip install --upgrade pip
export ENABLE_CONTRIB=1
pip wheel . --verbose
```

在使用自己编译的opencv时, 会报错
```bash
Traceback (most recent call last):
  File "qrcode.py", line 1, in <module>
    import cv2
  File "/media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/python3.7/site-packages/cv2/__init__.py", line 181, in <module>
    bootstrap()
  File "/media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/python3.7/site-packages/cv2/__init__.py", line 153, in bootstrap
    native_module = importlib.import_module("cv2")
  File "/media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/python3.7/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
ImportError: /usr/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0
```
解决方法为[1](https://blog.csdn.net/qq_38606680/article/details/129118491)和[2](https://zhuanlan.zhihu.com/p/630164701)
```bash
mv /media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/libffi.so.7 /media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/libffi.so.7.bak
ln -s /usr/lib/x86_64-linux-gnu/libffi.so.7.1.0  /media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/opencv/lib/libffi.so.7
```
