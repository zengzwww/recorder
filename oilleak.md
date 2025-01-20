# oilleak

## DetectorRS

### Trainning

```bash
CUDA_VISIBLE_DEVICES=0,1 ./tools/dist_train.sh configs/detectors/oilleak.py 2 --work-dir ../../experiments/oilleak --auto-scale-lr
```

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

解决办法见[1](https://github.com/open-mmlab/mmdetection/issues/10161)和[2](https://mmdetection.readthedocs.io/en/latest/advanced_guides/customize_dataset.html#modify-the-config-file-for-using-the-customized-dataset)
