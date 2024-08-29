# Python

## ERROR: Could not install packages due to an EnvironmentError: Missing dependencies for SOCKS support.

`/usr/bin/python3 -m pip install -U pycodestyle`时报错:  
`ERROR: Could not install packages due to an EnvironmentError: Missing dependencies for SOCKS support.`  

[解决办法](https://blog.csdn.net/whatday/article/details/109287343#:~:text=1%20Unset%20socks%20proxy%2C%20in%20your%20case%3A%20unset,and%20pip%20install%20works%20again%20with%20socks%20proxy.):
```bash
unset all_proxy && unset ALL_PROXY # 取消所有 socks 代理
pip install pysocks
```

## 修改python setup.py install的源

方法一：
修改文件 ~/.pydistutils.cfg为：
```text
[easy_install]
index_url = https://mirrors.aliyun.com/pypi/simple/
```
方法二：
直接在setup.py的同目录放置一个setup.cfg：
```text
[easy_install]
index_url = https://mirrors.aliyun.com/pypi/simple/
```

## Shapely

conda环境下用pip安装Shapely, 使用Shapely时报错
```text
DEBUG:shapely.geos:Found GEOS DLL: <CDLL '/media/dlyrm/Jingbo_datas/tseng/anaconda3/envs/boundary_patch_detection/lib/python3.7/site-packages/Shapely.libs/libgeos_c-74dec7a7.so.1.14.2', handle fc5f70 at 0x7f5360a4d5d0>, using it.
```

解决方法, 使用conda安装
```bash
conda install shapely
```

## conda activate error

```text
CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.
To initialize your shell, run

    $ conda init <SHELL_NAME>

Currently supported shells are:
  - bash
  - fish
  - tcsh
  - xonsh
  - zsh
  - powershell

See 'conda init --help' for more information and options.

IMPORTANT: You may need to close and restart your shell after running 'conda init'.
```

解决办法

```bash
source /path/to/anaconda3/etc/profile.d/conda.sh
```

## 删除__pycache__

```bash
find . -type d -name  "__pycache__" -exec rm -r {} +
```

## conda环境下：OSError: CUDA_HOME environment variable is not set. Please set it to your CUDA install root

```bash
export CUDA_HOME=$CONDA_PREFIX
```

参考[stackoverflow](https://stackoverflow.com/questions/46064433/cuda-home-path-for-tensorflow)

## conda环境下：conda nvcc: No such file or directory

安装cudatoolkit-dev，参考[stackoverflow](https://stackoverflow.com/questions/56470424/nvcc-missing-when-installing-cudatoolkit)

## Module level import not at top of file

[参考](https://stackoverflow.com/questions/36827962/pep8-import-not-at-top-of-file-with-sys-path)

## pip install报错：No space left on device

参考[博客](https://naoko.github.io/pip-install-no-space-left/)

```
export TMPDIR=/bigass/space
pip install ...
```

## Available platform plugins are: xcb, eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, wayland-egl, wayland, wayland-xcomposite-egl, wayland-xcomposite-glx, webgl

```text
2024-08-29 10:09:52,210 [INFO   ] __init__:get_config:67- Loading config file from: /home/industai/.labelmerc
QObject::moveToThread: Current thread (0x2247af0) is not the object's thread (0x38cdc00).
Cannot move to target thread (0x2247af0)

qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "/home/industai/miniconda3/envs/open-mmlab/lib/python3.8/site-packages/cv2/qt/plugins" even though it was found.
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

Available platform plugins are: xcb, eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, wayland-egl, wayland, wayland-xcomposite-egl, wayland-xcomposite-glx, webgl.

已放弃 (核心已转储)
```

先安装opencv-python, 再安装opencv-python-headless, 可解决该问题.
