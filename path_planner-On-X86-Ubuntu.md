$ sudo apt install libompl-dev    
$ mkdir -p ~/workspace/catkin/src  
$ cd ~/workspace/catkin/src/  
$ git clone https://github.com/karlkurzer/path_planner.git  
$ cd ..  
$ catkin_make  
Base path: /home/tseng/workspace/catkin  
Source space: /home/tseng/workspace/catkin/src  
Build space: /home/tseng/workspace/catkin/build  
Devel space: /home/tseng/workspace/catkin/devel  
Install space: /home/tseng/workspace/catkin/install  
####  
#### Running command: "cmake /home/tseng/workspace/catkin/src -DCATKIN_DEVEL_PREFIX=/home/tseng/workspace/catkin/devel -DCMAKE_INSTALL_PREFIX=/home/tseng/workspace/catkin/install -G Unix Makefiles" in "/home/tseng/workspace/catkin/build"
####  
-- Using CATKIN_DEVEL_PREFIX: /home/tseng/workspace/catkin/devel  
-- Using CMAKE_PREFIX_PATH: /opt/ros/noetic  
-- This workspace overlays: /opt/ros/noetic  
-- Using PYTHON_EXECUTABLE: /home/tseng/anaconda3/bin/python3  
-- Using Debian Python package layout  
-- Could NOT find PY_em (missing: PY_EM)   
CMake Error at /opt/ros/noetic/share/catkin/cmake/empy.cmake:30 (message):  
  Unable to find either executable 'empy' or Python module 'em'...  try  
  installing the package 'python3-empy'  
Call Stack (most recent call first):  
  /opt/ros/noetic/share/catkin/cmake/all.cmake:164 (include)  
  /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:20 (include)  
  CMakeLists.txt:58 (find_package)  


-- Configuring incomplete, errors occurred!  
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeOutput.log".  
Invoking "cmake" failed  

解决办法:  
$ sudo apt-get install python3-empy  
$ catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3  
