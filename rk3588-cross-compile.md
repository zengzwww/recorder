# aarch64.cmake

```
# the name of the target operating system
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR ARM)

# which compilers to use for C and C++
set(CMAKE_C_COMPILER   aarch64-linux-gnu-gcc-9)
set(CMAKE_CXX_COMPILER aarch64-linux-gnu-g++-9)

# where is the target environment located
set(CMAKE_FIND_ROOT_PATH /usr/aarch64-linux-gnu/bin)

# adjust the default behavior of the FIND_XXX() commands:
# search programs in the host environment
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)

# search headers and libraries in the target environment
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
```

# libusb-1.0

```
cd libusb
tar xvf libusb-1.0.26.tar.gz
mkdir build && cd build
sh ../libusb-1.0.26/autogen.sh \
CC=aarch64-linux-gnu-gcc-9 \
CXX=aarch64-linux-gnu-g++-9 \
--prefix=$(pwd)/../install \
--host=x86_64 \
--target=aarch64 \
--enable-shared=yes \
--enable-static=no
```
