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
