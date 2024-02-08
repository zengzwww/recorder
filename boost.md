# boost

## AARCH64

```bash
cd boost
tar jxvf boost_1_82_0.tar.bz2
cd boost_1_82_0/tools/build
./bootstrap.sh
./b2 install --prefix=$(pwd)/../../../tools
cd ../../
../tools/bin/b2 install --prefix=$(pwd)/../install --build-dir=$(pwd)/../build toolset=gcc stage
```
