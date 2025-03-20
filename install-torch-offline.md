# install torch offline

```bash
pip download torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --index-url https://download.pytorch.org/whl/cu118 -d torch-2.5.1-cu118-deps
```

```bash
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --no-index --find-links=$(pwd)torch-2.5.1-cu118-deps
```
