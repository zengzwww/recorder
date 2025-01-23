# oilleak

## DetectorRS

- HTC
```text
Cascade Mask R-CNN = Mask R-CNN +Cascade R-CNN，处理流程为，由RPN预测初始的矩形框，初始矩形框和CNN特征输入池化层，得到矩形框特征和遮罩特征，通过矩形框预测头和遮罩预测头预测本阶段的矩形框和遮罩，本阶段预测的矩形框可视为初始矩形框精细化的结果，继续将它和CNN特征一起输入下一阶段的池化层，得到下一阶段的矩形框特征和遮罩特征，然后按照同样的处理流程继续精细化矩形框预测和遮罩预测。这种方式结合了级联精细化的思想和矩形框预测和遮罩预测之间相互促进的优点，比Mask R-CNN和Cascade R-CNN的矩形框AP都要高。

Cascade Mask R-CNN的一个缺点是矩形框和遮罩分支并行执行，相互之间没有互动，因此，将并行执行改为交错执行，每个阶段都使用下一个阶段的遮罩特征来预测本阶段的遮罩，而下一阶段的遮罩特征是根据本阶段精细化预测的矩形框经池化得到的，所以两个分支有了互动。

还有一个问题是不同阶段遮罩分支之间没有直接的信息流，阻扰了遮罩预测精度的进一步提升，因此，将前一阶段遮罩预测头的中间特征和当前阶段的遮罩特征整合之后，再预测本阶段的遮罩，遮罩的预测也可以逐渐精细化。

最后，增加语义分割分支，通过空间上下文线索，进一步增强前景和复杂背景的区分能力，并且将语义特征与矩形框/遮罩特征，使不同分支之间有更多的相互作用，通过联合训练紧密关联的任务增强特征表达能力，提升原任务的性能。
```

- RFP
```text
递归金字塔RFP，本层本轮输出特征，为上一层本轮输出特征与本层骨干输出特征整合变换的结果，与FPN不同，本层骨干输出特征为下一层骨干输出特征与本层上一轮输出特征整合变换的结果，而不是下一层骨干输出特征变换之后的结果。本层本轮输出特征也取决于本层上一轮输出特征，蕴含递归运算的成分。下一层骨干输出特征与本层上一轮输出特征的整合变换发生在ResNet每个阶段的第一个残差块。本层上一轮输出特征在整合之前，需要先经过空洞空间金字塔池化ASPP变换，总共四个分支的其中三个使用不同膨胀率的卷积，另外一个使用全局平均池化，然后四个分支的结果经拼接得到输出特征。而上一层本轮输出特征在整合之前，其实融入了上一层上一轮输出特征，融合方式为注意力加权求和。
```

### Training

Build `configs/detectors/oilleak.py`:
```text
_base_ = '../htc/htc_r50_fpn_1x_coco.py'

######################################################################

_base_.model['roi_head']['bbox_head'][0]['num_classes'] = 6
_base_.model['roi_head']['bbox_head'][1]['num_classes'] = 6
_base_.model['roi_head']['bbox_head'][2]['num_classes'] = 6
_base_.model['roi_head']['mask_head'][0]['num_classes'] = 6
_base_.model['roi_head']['mask_head'][1]['num_classes'] = 6
_base_.model['roi_head']['mask_head'][2]['num_classes'] = 6
_base_.model['roi_head']['semantic_head']['num_classes'] = 6

######################################################################

classes = ('sly_bjbmyw', 'sly_bjbmyw_dry', 'sly_bjbmyw_susp', 'sly_dmyw', 'sly_dmyw_dry', 'sly_dmyw_susp')
data_root = '/data/zengzw/data/substation/oilleak/'

_base_.train_dataloader['dataset']['metainfo'] = dict(classes=classes)
_base_.train_dataloader['dataset']['data_root'] = data_root
_base_.train_dataloader['dataset']['ann_file'] = 'annotations/train.json'
_base_.train_dataloader['dataset']['data_prefix'] = dict(img='train/', seg='train_mask/')

_base_.val_dataloader['dataset']['metainfo'] = dict(classes=classes)
_base_.val_dataloader['dataset']['data_root'] = data_root
_base_.val_dataloader['dataset']['ann_file'] = 'annotations/val.json'
_base_.val_dataloader['dataset']['data_prefix'] = dict(img='val/', seg='val_mask/')

_base_.val_evaluator['ann_file'] = data_root + 'annotations/val.json'

_base_.test_dataloader = _base_.val_dataloader
_base_.test_evaluator = _base_.val_evaluator

######################################################################

load_from = '/data/zengzw/models/mmdetection/detectors_cascade_rcnn_r50_1x_coco-32a10ba0.pth'

######################################################################

model = dict(
    backbone=dict(
        type='DetectoRS_ResNet',
        conv_cfg=dict(type='ConvAWS'),
        sac=dict(type='SAC', use_deform=True),
        stage_with_sac=(False, True, True, True),
        output_img=True),
    neck=dict(
        type='RFP',
        rfp_steps=2,
        aspp_out_channels=64,
        aspp_dilations=(1, 3, 6, 1),
        rfp_backbone=dict(
            rfp_inplanes=256,
            type='DetectoRS_ResNet',
            depth=50,
            num_stages=4,
            out_indices=(0, 1, 2, 3),
            frozen_stages=1,
            norm_cfg=dict(type='BN', requires_grad=True),
            norm_eval=True,
            conv_cfg=dict(type='ConvAWS'),
            sac=dict(type='SAC', use_deform=True),
            stage_with_sac=(False, True, True, True),
            pretrained='torchvision://resnet50',
            style='pytorch')))
```

Training:
```bash
CUDA_VISIBLE_DEVICES=0,1 ./tools/dist_train.sh configs/detectors/oilleak.py 2 --work-dir ../../experiments/oilleak --auto-scale-lr
```

- Error 1

```text
Done (t=0.16s)
creating index...
index created!
Traceback (most recent call last):
  File "./tools/train.py", line 121, in <module>
    main()
  File "./tools/train.py", line 117, in main
    runner.train()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1728, in train
    self._train_loop = self.build_train_loop(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1520, in build_train_loop
    loop = LOOPS.build(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/registry.py", line 570, in build
    return self.build_func(cfg, *args, **kwargs, registry=self)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/build_functions.py", line 121, in build_from_cfg
    obj = obj_cls(**args)  # type: ignore
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 46, in __init__
    super().__init__(runner, dataloader)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/base_loop.py", line 26, in __init__
    self.dataloader = runner.build_dataloader(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1370, in build_dataloader
    dataset = DATASETS.build(dataset_cfg)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/registry.py", line 570, in build
    return self.build_func(cfg, *args, **kwargs, registry=self)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/build_functions.py", line 121, in build_from_cfg
    obj = obj_cls(**args)  # type: ignore
  File "/data/zengzw/codes/mmdetection/mmdet/datasets/base_det_dataset.py", line 51, in __init__
    super().__init__(*args, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/dataset/base_dataset.py", line 247, in __init__
    self.full_init()
  File "/data/zengzw/codes/mmdetection/mmdet/datasets/base_det_dataset.py", line 89, in full_init
    self.data_bytes, self.data_address = self._serialize_data()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/dataset/base_dataset.py", line 768, in _serialize_data
    data_bytes = np.concatenate(data_list)
  File "<__array_function__ internals>", line 200, in concatenate
ValueError: need at least one array to concatenate
loading annotations into memory...
Done (t=0.05s)
creating index...
index created!
Traceback (most recent call last):
  File "./tools/train.py", line 121, in <module>
    main()
  File "./tools/train.py", line 117, in main
    runner.train()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1728, in train
    self._train_loop = self.build_train_loop(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1520, in build_train_loop
    loop = LOOPS.build(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/registry.py", line 570, in build
    return self.build_func(cfg, *args, **kwargs, registry=self)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/build_functions.py", line 121, in build_from_cfg
    obj = obj_cls(**args)  # type: ignore
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 46, in __init__
    super().__init__(runner, dataloader)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/base_loop.py", line 26, in __init__
    self.dataloader = runner.build_dataloader(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1370, in build_dataloader
    dataset = DATASETS.build(dataset_cfg)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/registry.py", line 570, in build
    return self.build_func(cfg, *args, **kwargs, registry=self)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/registry/build_functions.py", line 121, in build_from_cfg
    obj = obj_cls(**args)  # type: ignore
  File "/data/zengzw/codes/mmdetection/mmdet/datasets/base_det_dataset.py", line 51, in __init__
    super().__init__(*args, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/dataset/base_dataset.py", line 247, in __init__
    self.full_init()
  File "/data/zengzw/codes/mmdetection/mmdet/datasets/base_det_dataset.py", line 89, in full_init
    self.data_bytes, self.data_address = self._serialize_data()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/dataset/base_dataset.py", line 768, in _serialize_data
    data_bytes = np.concatenate(data_list)
  File "<__array_function__ internals>", line 200, in concatenate
ValueError: need at least one array to concatenate
ERROR:torch.distributed.elastic.multiprocessing.api:failed (exitcode: 1) local_rank: 0 (pid: 196878) of binary: /data/miniconda3/envs/openmmlab/bin/python
Traceback (most recent call last):
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 196, in <module>
    main()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 192, in main
    launch(args)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 177, in launch
    run(args)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/run.py", line 785, in run
    elastic_launch(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 134, in __call__
    return launch_agent(self._config, self._entrypoint, list(args))
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 250, in launch_agent
    raise ChildFailedError(
torch.distributed.elastic.multiprocessing.errors.ChildFailedError: 
============================================================
./tools/train.py FAILED
------------------------------------------------------------
Failures:
[1]:
  time      : 2025-01-20_11:53:15
  host      : ai-172-20-60-12
  rank      : 1 (local_rank: 1)
  exitcode  : 1 (pid: 196879)
  error_file: <N/A>
  traceback : To enable traceback see: https://pytorch.org/docs/stable/elastic/errors.html
------------------------------------------------------------
Root Cause (first observed failure):
[0]:
  time      : 2025-01-20_11:53:15
  host      : ai-172-20-60-12
  rank      : 0 (local_rank: 0)
  exitcode  : 1 (pid: 196878)
  error_file: <N/A>
  traceback : To enable traceback see: https://pytorch.org/docs/stable/elastic/errors.html
============================================================
```

Solutions: [1](https://github.com/open-mmlab/mmdetection/issues/10161) and [2](https://mmdetection.readthedocs.io/en/latest/advanced_guides/customize_dataset.html#modify-the-config-file-for-using-the-customized-dataset)

- Error 2

```text
Traceback (most recent call last):
  File "./tools/train.py", line 121, in <module>
    main()
  File "./tools/train.py", line 117, in main
    runner.train()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1777, in train
    model = self.train_loop.run()  # type: ignore
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 98, in run
    self.run_epoch()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 115, in run_epoch
    self.run_iter(idx, data_batch)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 131, in run_iter
    outputs = self.runner.model.train_step(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/model/wrappers/distributed.py", line 121, in train_step
    losses = self._run_forward(data, mode='loss')
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/model/wrappers/distributed.py", line 161, in _run_forward
    results = self(**data, mode=mode)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1501, in _call_impl
    return forward_call(*args, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/parallel/distributed.py", line 1156, in forward
    output = self._run_ddp_forward(*inputs, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/parallel/distributed.py", line 1110, in _run_ddp_forward
    return module_to_run(*inputs[0], **kwargs[0])  # type: ignore[index]
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1501, in _call_impl
    return forward_call(*args, **kwargs)
  File "/data/zengzw/codes/mmdetection/mmdet/models/detectors/base.py", line 92, in forward
    return self.loss(inputs, data_samples)
  File "/data/zengzw/codes/mmdetection/mmdet/models/detectors/two_stage.py", line 190, in loss
    roi_losses = self.roi_head.loss(x, rpn_results_list,
  File "/data/zengzw/codes/mmdetection/mmdet/models/roi_heads/htc_roi_head.py", line 288, in loss
    gt_semantic_segs = [
  File "/data/zengzw/codes/mmdetection/mmdet/models/roi_heads/htc_roi_head.py", line 289, in <listcomp>
    data_sample.gt_sem_seg.sem_seg
  File "/data/zengzw/codes/mmdetection/mmdet/structures/det_data_sample.py", line 213, in gt_sem_seg
    return self._gt_sem_seg
AttributeError: 'DetDataSample' object has no attribute '_gt_sem_seg'
Traceback (most recent call last):
  File "./tools/train.py", line 121, in <module>
    main()
  File "./tools/train.py", line 117, in main
    runner.train()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/runner.py", line 1777, in train
    model = self.train_loop.run()  # type: ignore
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 98, in run
    self.run_epoch()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 115, in run_epoch
    self.run_iter(idx, data_batch)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/runner/loops.py", line 131, in run_iter
    outputs = self.runner.model.train_step(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/model/wrappers/distributed.py", line 121, in train_step
    losses = self._run_forward(data, mode='loss')
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/mmengine/model/wrappers/distributed.py", line 161, in _run_forward
    results = self(**data, mode=mode)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1501, in _call_impl
    return forward_call(*args, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/parallel/distributed.py", line 1156, in forward
    output = self._run_ddp_forward(*inputs, **kwargs)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/parallel/distributed.py", line 1110, in _run_ddp_forward
    return module_to_run(*inputs[0], **kwargs[0])  # type: ignore[index]
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1501, in _call_impl
    return forward_call(*args, **kwargs)
  File "/data/zengzw/codes/mmdetection/mmdet/models/detectors/base.py", line 92, in forward
    return self.loss(inputs, data_samples)
  File "/data/zengzw/codes/mmdetection/mmdet/models/detectors/two_stage.py", line 190, in loss
    roi_losses = self.roi_head.loss(x, rpn_results_list,
  File "/data/zengzw/codes/mmdetection/mmdet/models/roi_heads/htc_roi_head.py", line 288, in loss
    gt_semantic_segs = [
  File "/data/zengzw/codes/mmdetection/mmdet/models/roi_heads/htc_roi_head.py", line 289, in <listcomp>
    data_sample.gt_sem_seg.sem_seg
  File "/data/zengzw/codes/mmdetection/mmdet/structures/det_data_sample.py", line 213, in gt_sem_seg
    return self._gt_sem_seg
AttributeError: 'DetDataSample' object has no attribute '_gt_sem_seg'
ERROR:torch.distributed.elastic.multiprocessing.api:failed (exitcode: 1) local_rank: 0 (pid: 437108) of binary: /data/miniconda3/envs/openmmlab/bin/python
Traceback (most recent call last):
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 196, in <module>
    main()
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 192, in main
    launch(args)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launch.py", line 177, in launch
    run(args)
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/run.py", line 785, in run
    elastic_launch(
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 134, in __call__
    return launch_agent(self._config, self._entrypoint, list(args))
  File "/data/miniconda3/envs/openmmlab/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 250, in launch_agent
    raise ChildFailedError(
torch.distributed.elastic.multiprocessing.errors.ChildFailedError: 
============================================================
./tools/train.py FAILED
------------------------------------------------------------
Failures:
[1]:
  time      : 2025-01-20_16:14:14
  host      : ai-172-20-60-12
  rank      : 1 (local_rank: 1)
  exitcode  : 1 (pid: 437109)
  error_file: <N/A>
  traceback : To enable traceback see: https://pytorch.org/docs/stable/elastic/errors.html
------------------------------------------------------------
Root Cause (first observed failure):
[0]:
  time      : 2025-01-20_16:14:14
  host      : ai-172-20-60-12
  rank      : 0 (local_rank: 0)
  exitcode  : 1 (pid: 437108)
  error_file: <N/A>
  traceback : To enable traceback see: https://pytorch.org/docs/stable/elastic/errors.html
```

Solutions: [1](https://github.com/open-mmlab/mmdetection/issues/10613)

### Testing

```bash
python tools/test.py configs/detectors/oilleak.py ../../experiments/oilleak/epoch_12.pth --work-dir ../../experiments/oilleak --show-dir ./test --out ../../experiments/oilleak/test.pkl
```
