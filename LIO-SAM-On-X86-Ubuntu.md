1 安装依赖包  
sudo apt-get install -y ros-noetic-navigation  
sudo apt-get install -y ros-noetic-robot-localization  
sudo apt-get install -y ros-noetic-robot-state-publisher  

sudo add-apt-repository ppa:borglab/gtsam-release-4.0  
sudo apt install libgtsam-dev libgtsam-unstable-dev  

2 安装LIO-SAM  
cd /pth/to/catkin/src
git clone https://github.com/TixiaoShan/LIO-SAM.git
cd ..
catkin_make -j1

报错, 需要修改一些东东  
修改CMakeLists.txt及源码  
$ git diff  
diff --git a/CMakeLists.txt b/CMakeLists.txt  
index f96b004..f00ff11 100644  
--- a/CMakeLists.txt   
+++ b/CMakeLists.txt  
@@ -2,8 +2,8 @@ cmake_minimum_required(VERSION 2.8.3)  
 project(lio_sam)  
 
 set(CMAKE_BUILD_TYPE "Release")  
-set(CMAKE_CXX_FLAGS "-std=c++11")  
-set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread")  
+set(CMAKE_CXX_FLAGS "-std=c++14")  
+set(CMAKE_CXX_FLAGS_RELEASE "-std=c++14 -O3 -Wall -g -pthread")  
 
 find_package(catkin REQUIRED COMPONENTS  
   tf  
diff --git a/include/utility.h b/include/utility.h  
index cc3c60f..64c8b9f 100644  
--- a/include/utility.h  
+++ b/include/utility.h  
@@ -15,7 +15,8 @@  
 #include <visualization_msgs/Marker.h>  
 #include <visualization_msgs/MarkerArray.h>  
 
-#include <opencv/cv.h>  
+#include <flann/flann.hpp>  
+#include <opencv2/opencv.hpp>  
 
 #include <pcl/point_cloud.h>  
 #include <pcl/point_types.h>  

3 运行  
开一个终端  
$ cd /path/to/catkin  
$ source devel/setup.bash  
$ roslaunch lio_sam run.launch  
开第二个终端  
$ cd /path/to/catkin  
$ source devel/setup.bash  
$ rosbag play /mnt/host/downloads/lio_sam/walking_dataset.bag -r 3  

4 保存地图  
$ cd /path/to/catkin   
$ source devel/setup.bash  
$ rosservice call /lio_sam/save_map 0.2 /Downloads/  
这里的路径是用户路径下的路径, 不存在不会有结果输出  

5 查看地图  
$ sudo apt-get install  pcl-tools  
$ pcl_viewer Downloads/GlobalMap.pcd  
