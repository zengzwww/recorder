# OpenVINO

## 查看可用的设备
```bash
python -c "from openvino.runtime import Core; print(Core().available_devices)"
```
或者
```bash
python -c "from openvino.inference_engine import IECore; print(IECore().available_devices)"
```

## 如何配置GPU？
[需要安装对应的显卡驱动](https://docs.openvino.ai/2022.3/openvino_docs_install_guides_configurations_for_intel_gpu.html)

## 如何量化?
参考[POT技术](https://docs.openvino.ai/2023.0/pot_default_quantization_usage.html)
