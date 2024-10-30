# ComfyUI实操

## 安装

```bash
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
git submodule add -f https://github.com/ltdrdata/ComfyUI-Manager.git custom_nodes/ComfyUI-Manager
```

## 运行

```bash
python main.py --listen 0.0.0.0
```
## 模型

- [cyberrealistic_v42.safetensors](https://civitai.com/models/15003?modelVersionId=198401)
- [latent-consistency/lcm-lora-sdv1-5](https://huggingface.co/latent-consistency/lcm-lora-sdv1-5)
- [stable-diffusion-v1-5/stable-diffusion-inpainting](https://huggingface.co/stable-diffusion-v1-5/stable-diffusion-inpainting)

## 提示词

### human

```text
Cannon EOS 5D MARK III, 50mm Sigma f/1.4 ZEISS lens, F1.4, 1/800s, ISO 100, RAW photo, (photorealistic:1.4), 8k uhd, film grain, cinematic lighting, masterpiece, best quality,  (ulzzang-6500:0.5), 1 girl, beautiful korean girl, kpop idol, ((full body)), slim figure, fair skin, very sexy and charming, white t-shirt, red silk pants, long hair, (perfect face:1.1), (eyelashes:1.1), (perfect eyes:1.1), (big breasts:1.2), toned stomach, beautiful hips, slender thighs, standing, looking ahead
```
