参考[rk3588上安装librealsense](https://github.com/IntelRealSense/librealsense/issues/11030),[NVIDIA Jetson installation](https://dev.intelrealsense.com/docs/nvidia-jetson-tx2-installation)和[libuvc_installation.sh](https://github.com/IntelRealSense/librealsense/blob/master/scripts/libuvc_installation.sh)
```
sudo apt-get update
sudo apt-get install aptitude
sudo aptitude install git cmake libssl-dev freeglut3-dev libusb-1.0-0-dev pkg-config libgtk-3-dev unzip
mkdir ~/Downloads/librealsense
把librealsense-2.52.1.tar.gz放到此目录下
cd ~/Downloads/librealsense
tar xvf librealsense-2.52.1.tar.gz
cd librealsense-2.52.1
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
cd ..
sudo udevadm control --reload-rules && sudo udevadm trigger
mkdir build && cd build
cmake -DBUILD_EXAMPLES=true \
-DCMAKE_BUILD_TYPE=release \
-DFORCE_RSUSB_BACKEND=true \
-DBUILD_SHARED_LIBS=OFF \
-DCMAKE_INSTALL_PREFIX=$(pwd)/../install \
../librealsense-2.52.1
make -j4
sudo make install
```
编译出来的bin目录下的文件非常大, 用[strip](https://github.com/IntelRealSense/librealsense/issues/3211)命令去除调式等信息. [不要对库文件strip!](https://github.com/emscripten-core/emscripten/issues/9705)  

如何集成到CMake工程中?  
```
set(realsense2_DIR ${CMAKE_CURRENT_LIST_DIR}/3rdparty/librealsense/lib/cmake/realsense2)
find_package(realsense2 REQUIRED)
include_directories(${realsense2_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} ${realsense2_LIBRARY} pthread)
```
