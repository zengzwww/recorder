# install torch offline

```bash
pip download torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --index-url https://download.pytorch.org/whl/cu118 -d ultralytics-8.3.87-deps
```

```bash
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --no-index --find-links=$(pwd)/ultralytics-8.3.87-deps/
```
