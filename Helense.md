# Helense

## 更新pip源

```bash
mkdir ~/.pip
gedit ~/.pip/pip.conf
```

文件里面的内容为
```
[global]
index-url = https://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```

## 开启蒲公英VPN

```
pgyvisitor login
```
输入账号或UID回车，然后输入密码回车. 登出账号为:
```
pgyvisitor logout
```

## gRPC

安装命令为
```bash
pip install protobuf==3.14.0
pip install grpcio==1.36.1
pip install grpcio-tools==1.36.1
pip install opencv-python==4.5.3.56
```

### 测试程序grpc_demo

修改/添加proto文件, 编译proto生成python接口文件

```bash
cd grpc_demo/api/proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. *.proto
```

改一改源码:   
将`api.proto`中`import "common.proto";`改为`from . import "common.proto";`   
将`api_pb2.py`中`import common_pb2 as common__pb2`改为`from . import common_pb2 as common__pb2`   
将`api_pb2_grpc.py`中`import api_pb2 as api__pb2`改为`from . import api_pb2 as api__pb2`   

然后开两个终端分别执行服务器端
```bash
python examples/run_server.py
```
和客户端
```bash
python examples/run_client.py
```

### gRPC服务器interface_grpc

修改/添加proto文件, 编译proto生成python接口文件

```bash
cd interface_grpc/api/proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. common/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. v1/platform/*.proto
python -m grpc_tools.protoc -I ./ --python_out=. --grpc_python_out=. v1/device/*.proto
```

服务器端执行
```bash
python examples/run_step2.py
```

将盒子上算法配置文件(xxx_config.json)中的`grpc_ip_port`的IP设置为服务器的IP, 然后在盒子上运行算法, 服务器端就会收到报警信息

## 以服务形式跑算法

将盒子上算法配置文件中的`debug`设置为`false`, 新建`xxx@.service`文件, 其中的内容为
```
[Unit]
Description=People Invasion Detection Service

[Service]
Environment="SCRIPT_ARGS=%I"
ExecStart=/bin/bash /path/to/run_xxx.sh $SCRIPT_ARGS
ExecReload=/bin/kill -HUP $MAINPID
KillSignal=SIGINT
Restart=always
RestartSec=1s
IgnoreSIGPIPE=no
StandardOutput=syslog
StandardError=inherit

[Install]
WantedBy=multi-user.target
```

@表示该算法服务带参数, 如果不带参数则去除@(包括下面出现的@)

新建文件`/path/to/run_xxx.sh`, 其中的内容为
```
args="$@"
source /opt/intel/openvino_2021/bin/setupvars.sh

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/aimall/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/aimall/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home/aimall/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/aimall/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

conda activate helens

export LD_LIBRARY_PATH=/home/aimall/deploy/helens/algo/imo_core:$LD_LIBRARY_PATH

cd /path/to/xxx
python -c "from run2 import main; main()" --config $args
```

注册算法服务
```bash
sudo cp xxx@.service /etc/systemd/system
sudo systemctl daemon-reload
```

启动/重启/停止/查看算法服务
```
sudo systemctl start xxx@"/path/to/xxx_config.json".service
sudo systemctl restart xxx@"/path/to/xxx_config.json".service
sudo systemctl stop xxx@"/path/to/xxx_config.json".service
sudo systemctl status xxx@"/path/to/xxx_config.json".service
```

查询算法服务运行日志
```bash
journalctl -u xxx@"/path/to/xxx_config.json".service -f -n 1000
```

设置开机启动算法服务
```bash
sudo systemctl enable xxx.service
```

## 平台主页

[主页](https://helensbar2.cus.aimall-tech.com/), 用户名: 17777777777, 密码: aimall@2018sf

## OpenVINO

安装OpenVINO, ubuntu环境下
```
tar -xvzf l_openvino_toolkit_p_2021.4.752.tgz
cd l_openvino_toolkit_p_2021.4.752
sudo ./install.sh
sudo ./install_openvino_dependencies.sh
```

配置环境变量
```bash
vim ~/.bashrc
```

添加
```
source /opt/intel/openvino_2021/bin/setupvars.sh
```

配置模型优化器
```bash
cd /opt/intel/openvino_2021/deployment_tools/model_optimizer/install_prerequisites
sudo ./install_prerequisites_onnx.sh
```

安装依赖项
```
conda create -n openvino python=3.7
pip install numpy==1.19
pip install networkx==2.5.1
pip install defusedxml
pip install onnx
pip install requests
```

以yolov5m为例，将ONNX格式模型转换为OpenVINO格式, windows环境下
```
python mo.py --input_model C:\Users\tseng\Downloads\yolov5m5.0.onnx --data_type FP16 --output_dir C:\Users\tseng\Downloads\openvino --input_shape "(1,3,640,640)" --mean_values "images(0,0,0)" --scale_values "images(255,255,255)"
```
ubuntu环境下
```
cd /opt/intel/openvino_2021/deployment_tools/model_optimizer
python mo.py --input_model /home/tseng/workspace/downloads/yolov5m5.0.onnx --data_type FP16 --output_dir /home/tseng/workspace/downloads/openvino --input_shape "(1,3,640,640)" --mean_values "images(0,0,0)" --scale_values "images(255,255,255)"
```

## 算法打包

假设所有包在根目录ROOT下.

### 安装imo-core

从/nas/research/deploy/imo_core/imo_core_4.1.9.zip下载imo_core_4.1.9.zip到$ROOT目录

```bash
cd $ROOT
unzip imo_core_4.1.9.zip
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd)/imo_core
```

### 编译cy_imo_core

安装Cython
```bash
pip install Cython
```

打开cy_imo_core/src/setup.py, 在library_dirs中添加`'../../imo_core'`

```bash
cd $ROOT
git clone git@git.aimall-tech.com:Research/Algorithm/general/cy_imo_core.git --recurse-submodules
cd cy_imo_core
./build.sh
```

### 编译people_invasion_detection_client

```bash
cd $ROOT
git clone git@git.aimall-tech.com:product/vsm/helensbar/device/people_invasion_detection_client.git --recurse-submodules
cp cy_imo_core/bootstrap.so people_invasion_detection_client/template_client/py_imo_core/cy_imo_core
cd people_invasion_detection_client
```

将setup_utils.py放到people_invasion_detection_client目录下, 并在该目录下新建config.py, 内容为

```
configs = {
    'name': 'people_invasion_detection_client',
    'version': '0.1.0',
    'main_path': 'configs/auth.py',
    'so_build_dir': 'release/people_invasion_detection_client',
    'copy_dirs': [
        'template_client/py_imo_core/cy_imo_core/bootstrap.so',
        'configs/default.json',
        'configs/default-openvino.json',
        'README.md',
    ]
}
```

编译

```bash
python setup_utils.py
```

## 算法资源配置

E类算法最多只能跑16路不同的视频   

设置CPU频率
```
sudo cpufreq-set
```


