# kubectl

```text
kubectl -n sentry cp /home/industai/zengzw/codes/all srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/bin/nd_demo srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai/negative_detection/bin
cp /home/industai/zengzw/codes/innoai/negative_detection/lib/libnegative_detect.so.1.0.0 /home/industai/zengzw/codes/innoai/negative_detection/lib/libnegative_detect.so.CUDA
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/lib/libnegative_detect.so.CUDA srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/usr/local/pkg/negative_detection/amd64/lib
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/config/algo_test.json srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai/negative_detection/config
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/config/point.json srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai/negative_detection/config
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/config/algo.json srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai/negative_detection/config

LD_LIBRARY_PATH=/usr/local/pkg/libtorch/amd64/libtorch/lib:$LD_LIBRARY_PATH ./nd_demo --algo=../config/algo_test.json --img_dir=../../../all --repeats=1 --save_dir=../../../all_nd/ --threads=4
LD_LIBRARY_PATH=/usr/local/pkg/libtorch/amd64/libtorch/lib:$LD_LIBRARY_PATH gdb ./nd_demo
set args --algo=../config/algo.json --img_dir=../../../all --repeats=1 --save_dir=../../../all_nd/ --threads=4

kubectl -n sentry cp /home/industai/zengzw/codes/innoai/negative_detection/lib/libnegative_detect.so.1.0.0 srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/home/industai/zengzw/codes/innoai/negative_detection/bin
LD_LIBRARY_PATH=$(pwd):/usr/local/pkg/libtorch/amd64/libtorch/lib:$LD_LIBRARY_PATH ./nd_demo --algo=../config/algo_test.json --img_dir=../../../all --repeats=1 --save_dir=../../../all_nd/ --threads=4
LD_LIBRARY_PATH=$(pwd):/usr/local/pkg/libtorch/amd64/libtorch/lib:$LD_LIBRARY_PATH gdb ./nd_demo
set args --algo=../config/algo.json --img_dir=../../../all --repeats=1 --save_dir=../../../all_nd/ --threads=4


kubectl -n sentry cp /home/industai/zengzw/codes/all/00000021_2号主变油枕瓦斯继电器外观_巡视原图.jpg
/home/industai/zengzw/codes/all/00000021_2号主变油枕瓦斯继电器外观_巡视原图.jpg


kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models/classification-glass/TorchScript_CUDA/classification-glass-GPU.torchscript srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/usr/local/pkg/engine_classification_glass/amd64/engine/TorchScript_CUDA
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models/classification-shell/TorchScript_CUDA/classification-shell-GPU.torchscript srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/usr/local/pkg/engine_classification-shell/amd64/engine/TorchScript_CUDA
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models/classification-silibar/TorchScript_CUDA/classification-silibar-GPU.torchscript srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/usr/local/pkg/engine_classification-silibar/amd64/engine/TorchScript_CUDA
kubectl -n sentry cp /home/industai/zengzw/codes/innoai/models/classification-oilseal/TorchScript_CUDA/classification-oilseal-GPU.torchscript srv-ai-adapter--gpu-5dc7f96cc8-qgvr8:/usr/local/pkg/engine_classification-oilseal/amd64/engine/TorchScript_CUDA


kubectl -n sentry get po
kubectl apply -f srv-ai-adapter--gpu.yml
kubectl -n sentry edit deploy srv-ai-adapter--gpu
kubectl -n sentry exec -it srv-ai-adapter--gpu-5dc7f96cc8-qgvr8 /bin/bash
cd /usr/local/pkg/bdz_wrapper/amd64/bin/



sudo nano /etc/apt/sources.list

Add this line at the end of the file:
deb http://th.archive.ubuntu.com/ubuntu jammy main 

apt update && apt install libc6
```
