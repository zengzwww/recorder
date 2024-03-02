# NVIDIA

## Upgrade graphic driver

Disable the GUI and reboot
```bash
sudo systemctl set-default multi-user.target
sudo reboot 0
```

Install the driver
```bash
sudo ./NVIDIA-Linux-x86_64-440.44.run
```

Enable the GUI and reboot
```bash
sudo systemctl set-default graphical.target
sudo reboot 0
```

[see](https://unix.stackexchange.com/questions/440840/how-to-unload-kernel-module-nvidia-drm)

## Maximizing NVIDIA GPU performance on Linux

see performance
```bash
nvidia-smi -q -d PERFORMANCE
```

[see](https://justin.palpant.us/monitor-and-maximize-nvidia-gpu-performance-on-linux/)

## Install cuda, cudnn, and tensorrt

cuda
```bash
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run
```
