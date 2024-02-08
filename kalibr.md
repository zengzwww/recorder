# build kalibr

## 缺少empy

..........................................................................................................................................................................................................  
Failed     << python_module:cmake                           [ Exited with code 1 ]                                                                                                                        
__________________________________________________________________________________________________________________________________________________________________________________________________________  
Errors     << aslam_time:cmake /home/tseng/workspace/kalibr_workspace/logs/aslam_time/build.cmake.000.log                                                                                                 
CMake Error at /opt/ros/noetic/share/catkin/cmake/empy.cmake:30 (message):  
  Unable to find either executable 'empy' or Python module 'em'...  try  
  installing the package 'python3-empy'  
Call Stack (most recent call first):  
  /opt/ros/noetic/share/catkin/cmake/all.cmake:164 (include)  
  /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:20 (include)  
  CMakeLists.txt:4 (find_package)  

解决办法：  
conda install -c conda-forge empy  

## 缺少catkin_pkg

..........................................................................................................................................................................................................  
Failed     << aslam_time:cmake                              [ Exited with code 1 ]                                                                                                                        
Failed    <<< aslam_time                                    [ 0.6 seconds ]                                                                                                                               
__________________________________________________________________________________________________________________________________________________________________________________________________________  
Errors     << ethz_apriltag2:cmake /home/tseng/workspace/kalibr_workspace/logs/ethz_apriltag2/build.cmake.001.log                                                                                         
ImportError: "from catkin_pkg.package import parse_package" failed: No module named 'catkin_pkg'  
Make sure that you have installed "catkin_pkg", it is up to date and on the PYTHONPATH.  
CMake Error at /opt/ros/noetic/share/catkin/cmake/safe_execute_process.cmake:11 (message):  
  execute_process(/home/tseng/anaconda3/envs/rk3588/bin/python3  
  "/opt/ros/noetic/share/catkin/cmake/parse_package_xml.py"  
  "/opt/ros/noetic/share/catkin/cmake/../package.xml"  
  "/home/tseng/workspace/kalibr_workspace/build/ethz_apriltag2/catkin/catkin_generated/version/package.cmake")  
  returned error code 1  
Call Stack (most recent call first):  
  /opt/ros/noetic/share/catkin/cmake/catkin_package_xml.cmake:74 (safe_execute_process)  
  /opt/ros/noetic/share/catkin/cmake/all.cmake:168 (_catkin_package_xml)  
  /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:20 (include)  
  CMakeLists.txt:6 (find_package)  

解决办法：  
pip install catkin-pkg  

## 缺少numpy/arrayobject.h

In file included from /home/tseng/workspace/kalibr_workspace/src/kalibr/Schweizer-Messer/numpy_eigen/src/autogen_module/numpy_eigen_export_module.cpp:2:  
/home/tseng/workspace/kalibr_workspace/src/kalibr/Schweizer-Messer/numpy_eigen/include/numpy_eigen/NumpyEigenConverter.hpp:21:10: fatal error: numpy/arrayobject.h: No such file or directory  
   21 | #include <numpy/arrayobject.h>  
      |          ^~~~~~~~~~~~~~~~~~~~~  
compilation terminated.  
make[2]: *** [CMakeFiles/numpy_eigen.dir/build.make:63: CMakeFiles/numpy_eigen.dir/src/autogen_module/numpy_eigen_export_module.cpp.o] Error 1  
make[1]: *** [CMakeFiles/Makefile2:340: CMakeFiles/numpy_eigen.dir/all] Error 2  
make: *** [Makefile:141: all] Error 2  

解决办法：  
sudo apt-get install python-numpy  

## 内存不足

fatal error: Killed signal terminated program cc1plus  

解决办法：  
减少编译的线程数  
catkin build -DCMAKE_BUILD_TYPE=Release -j3

## 缺少yaml  

(rk3588) tseng@tseng-VirtualBox:~/workspace/kalibr_workspace$ rosrun kalibr kalibr_bagcreater --help   
ModuleNotFoundError: No module named 'yaml'  

解决办法：  
pip3 install PyYAML  

## 缺少Cryptodome

(rk3588) tseng@tseng-VirtualBox:~/workspace/kalibr_workspace$ rosrun kalibr kalibr_bagcreater --help 
ModuleNotFoundError: No module named 'Cryptodome'  

解决办法：  
pip3 install pycryptodomex  

## 缺少gnupg

(rk3588) tseng@tseng-VirtualBox:~/workspace/kalibr_workspace$ rosrun kalibr kalibr_bagcreater --help 
ModuleNotFoundError: No module named 'gnupg'

解决办法：  
pip3 install gnupg  

## 缺少rospkg

(rk3588) tseng@tseng-VirtualBox:~/workspace/kalibr_workspace$ rosrun kalibr kalibr_bagcreater --help 
ModuleNotFoundError: No module named 'rospkg'

解决办法：  
pip3 install rospkg  


## 缺少wx

rosrun kalibr kalibr_calibrate_cameras --help
No module named 'wx'

解决办法：  

https://blog.51cto.com/wuhaoshu/429952   

sudo apt-get install libgtk-3-dev  
export PKG_CONFIG=/usr/bin/pkg-config  
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/lib/x86_64-linux-gnu/pkgconfig  
pip3 install wxPython  

## 缺少igraph

ModuleNotFoundError: No module named 'igraph'  

解决办法：   
pip3 install python-igraph  

