# cvat

## Run

远程访问[Set CVAT hostname and version](https://opencv.github.io/cvat/docs/faq/#how-to-change-default-cvat-hostname-or-port)

```bash
CVAT_HOST=172.20.40.13 CVAT_VERSION=v2.31.0 docker compose up -d
```

挂载本地目录

```bash
CVAT_HOST=172.20.40.13 CVAT_VERSION=v2.31.0 docker compose -f docker-compose.override.yml -f docker-compose.yml up -d
```
访问主页

```text
http://172.20.40.13:8080/auth/login
```

## 部署SAM

- 部署[支持serverless的CVAT](https://docs.cvat.ai/docs/administration/advanced/installation_automatic_annotation/)

```bash
CVAT_HOST=172.20.40.13 CVAT_VERSION=v2.31.0 docker compose -f docker-compose.yml -f components/serverless/docker-compose.serverless.yml up -d
```

停止该服务

```bash
CVAT_HOST=172.20.40.13 CVAT_VERSION=v2.31.0 docker compose -f docker-compose.yml -f components/serverless/docker-compose.serverless.yml down
```

- 安装nuctl

```bash
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-linux-amd64
sudo chmod +x nuctl-1.13.0-linux-amd64
sudo ln -sf $(pwd)/nuctl-<version>-linux-amd64 /usr/local/bin/nuctl
```

- 部署GPU版SAM

[参考](https://www.cvat.ai/resources/blog/facebook-segment-anything-model-in-cvat)

```bash
./serverless/deploy_gpu.sh ./serverless/pytorch/facebookresearch/sam/nuclio/
```

报错

```text
25.04.03 18:43:11.408 (I)                     nuctl Project created {"Name": "cvat", "Namespace": "nuclio"}                                                                                                                                                                       
Deploying pytorch/facebookresearch/sam function...                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                  
Error - Function cannot be updated when existing function is being provisioned                                                                                                                                                                                                    
    /nuclio/pkg/platform/local/platform.go:221                                                                                                                                                                                                                                    
                                                                                                                                                                                                                                                                                  
Call stack:                                                                                                                                                                                                                                                                       
Failed to validate a function configuration against an existing configuration                                                                                                                                                                                                     
    /nuclio/pkg/platform/local/platform.go:221                                                                                                                                                                                                                                    
(substation) industai@industai-Super-Server:/mnt/data/zengzw/codes/cvat$ ./serverless/deploy_gpu.sh ./serverless/pytorch/facebookresearch/sam/nuclio/                                                                                                                             
25.04.07 09:16:42.370 (I)                     nuctl Project created {"Name": "cvat", "Namespace": "nuclio"}                                                                                                                                                                       
Deploying pytorch/facebookresearch/sam function...                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                  
Error - Function cannot be updated when existing function is being provisioned                                                           
    /nuclio/pkg/platform/local/platform.go:221                                                                                           
                                                                                                                                         
Call stack:                                                                                                                                                                                                                                                                       
Failed to validate a function configuration against an existing configuration                                                                                                                                                                                                     
    /nuclio/pkg/platform/local/platform.go:221
```

[解决办法](https://stackoverflow.com/questions/76546895/function-cannot-be-deleted-as-it-is-being-provisioned)

```bash
nuctl delete function pth-facebookresearch-sam-vit-h --platform local --force
```

报错

```text
#9 [ 5/13] RUN pip3 install git+https://github.com/facebookresearch/segment-anything.git                                                                                                                                                                                          
#9 0.742 Collecting git+https://github.com/facebookresearch/segment-anything.git                                                                                                                                                                                                  
#9 0.742   Cloning https://github.com/facebookresearch/segment-anything.git to /tmp/pip-req-build-j5bq_ydp                                                                                                                                                                        
#9 0.746   Running command git clone --filter=blob:none --quiet https://github.com/facebookresearch/segment-anything.git /tmp/pip-req-build-j5bq_ydp                                                                                                                              
#9 131.6   fatal: unable to access 'https://github.com/facebookresearch/segment-anything.git/': Failed to connect to github.com port 443 after 130874 ms: Connection timed out                                                                                                    
#9 131.7   error: subprocess-exited-with-error                                                                                                                                                                                                                                    
#9 131.7                                                                                                                                                                                                                                                                          
#9 131.7   × git clone --filter=blob:none --quiet https://github.com/facebookresearch/segment-anything.git /tmp/pip-req-build-j5bq_ydp did not run successfully.                                                                                                                  
#9 131.7   │ exit code: 128                                                                                                                                                                                                                                                       
#9 131.7   ╰─> See above for output.                                                                                                                                                                                                                                              
#9 131.7                                                                                                                                                                                                                                                                          
#9 131.7   note: This error originates from a subprocess, and is likely not a problem with pip.                                                                                                                                                                                   
#9 131.7 error: subprocess-exited-with-error                                                                                                                                                                                                                                      
#9 131.7                                                                                                                                                                                                                                                                          
#9 131.7 × git clone --filter=blob:none --quiet https://github.com/facebookresearch/segment-anything.git /tmp/pip-req-build-j5bq_ydp did not run successfully.                                                                                                                    
#9 131.7 │ exit code: 128                                                                                                                                                                                                                                                         
#9 131.7 ╰─> See above for output.                                                                                                                                                                                                                                                
#9 131.7                                                                                                                                                                                                                                                                          
#9 131.7 note: This error originates from a subprocess, and is likely not a problem with pip.                                                                                                                                                                                     
#9 ERROR: process "/bin/sh -c pip3 install git+https://github.com/facebookresearch/segment-anything.git" did not complete successfully: exit code: 1                                                                                                                              
------                                                                                                                                                                                                                                                                            
 > [ 5/13] RUN pip3 install git+https://github.com/facebookresearch/segment-anything.git:                                                                                                                                                                                         
131.7   ╰─> See above for output.                                                                                                                                                                                                                                                 
131.7                                                                                                                                                                                                                                                                             
131.7   note: This error originates from a subprocess, and is likely not a problem with pip.                                                                                                                                                                                      
131.7 error: subprocess-exited-with-error                                                                                                                                                                                                                                         
131.7                                                                                                                                                                                                                                                                             
131.7 × git clone --filter=blob:none --quiet https://github.com/facebookresearch/segment-anything.git /tmp/pip-req-build-j5bq_ydp did not run successfully.                                                                                                                       
131.7 │ exit code: 128                                                                                                                                                                                                                                                            
131.7 ╰─> See above for output.                                                                                                                                                                                                                                                   
131.7                                                                                                                                                                                                                                                                             
131.7 note: This error originates from a subprocess, and is likely not a problem with pip.                                                                                                                                                                                        
------                                                                                                                                                                                                                                                                            
Dockerfile.processor:30                                                                                                                                                                                                                                                           
--------------------                                                                                                                                                                                                                                                              
  28 |     RUN pip3 install torch torchvision torchaudio pycocotools matplotlib onnxruntime onnx                                                                                                                                                                                  
  29 |                                                                                                                                                                                                                                                                            
  30 | >>> RUN pip3 install git+https://github.com/facebookresearch/segment-anything.git                                                                                                                                                                                          
  31 |                                                                                                                                   
  32 |     RUN curl -O https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth                                              
--------------------                                                                                                                     
ERROR: failed to solve: process "/bin/sh -c pip3 install git+https://github.com/facebookresearch/segment-anything.git" did not complete successfully: exit code: 1                                                                                                                
                                                                                                                                                                                                                                                                                  
    /nuclio/pkg/cmdrunner/shellrunner.go:114                                                                                             
Failed to build                                                                                                                          
    /nuclio/pkg/dockerclient/shell.go:119                                                                                                                                                                                                                                         
Failed to build docker image                                                                                                                                                                                                                                                      
    .../pkg/containerimagebuilderpusher/docker.go:70                                                                                                                                                                                                                              
Failed to build processor image                                                                                                                                                                                                                                                   
    /nuclio/pkg/processor/build/builder.go:267                                                                                                                                                                                                                                    
Failed to deploy function                                                                                                                                                                                                                                                         
    ...//nuclio/pkg/platform/abstract/platform.go:227
```

添加代理, 打开文件cvat/serverless/pytorch/facebookresearch/sam/nuclio/function-gpu.yaml, 在preCopy这里添加代理的环境变量

```text
        - kind: ENV
          value: HTTP_PROXY=http://127.0.0.1:8001
        - kind: ENV
          value: HTTPS_PROXY=http://127.0.0.1:8001
```
