# mmpretrain

#### 配置文件
利用_base_继承配置文件原型，在修改继承的域的时候要注意，如果修改了域A，然后之后的域B又用到了域A，必须在B中重新设置A，否则修改之后的A不会在B中生效。比如：
```text
vis_backends = [dict(type='LocalVisBackend'), dict(type='TensorboardVisBackend')]
visualizer = dict(type='UniversalVisualizer', vis_backends=vis_backends)
```
在vis_backends中添加了tensorboard后端，那么后面的visualizer也得重新设置vis_backends。  
配置文件必须放置在mmpretrain/configs/some_folder目录下。
