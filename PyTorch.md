# PyTorch

* AttributeError: module 'distutils' has no attribute 'version'  
PyTorch版本1.10，安装完tensorboard后运行代码时出现错误：AttributeError: module 'distutils' has no attribute 'version'。  
这是setuptools版本问题。  
解决方法为
```bash
pip uninstall setuptools
pip install setuptools==59.5.0
```
