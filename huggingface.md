# huggingface

## Download folder

1. Install git-lfs

```bash
sudo apt install git-lfs
git lfs install
git clone https://huggingface.co/liuhaotian/llava-v1.6-vicuna-7b # Not work
```

2. [Clone empty folder first](https://blog.iamdev.cn/post/2023/%E5%A6%82%E4%BD%95%E4%BC%98%E9%9B%85%E7%9A%84%E4%B8%8B%E8%BD%BDhuggingface%E7%9A%84%E5%A4%A7%E6%A8%A1%E5%9E%8B/)

```bash
git clone --depth 1 --branch main --no-checkout git@hf.co:liuhaotian/llava-v1.6-vicuna-7b
cd llava-v1.6-vicuna-7b
git checkout main # Not work
```
