$ git clone https://github.com/ros-planning/navigation
$ catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
Base path: /home/tseng/workspace/catkin
Source space: /home/tseng/workspace/catkin/src
Build space: /home/tseng/workspace/catkin/build
Devel space: /home/tseng/workspace/catkin/devel
Install space: /home/tseng/workspace/catkin/install
####
#### Running command: "cmake /home/tseng/workspace/catkin/src -DPYTHON_EXECUTABLE=/usr/bin/python3 -DCATKIN_DEVEL_PREFIX=/home/tseng/workspace/catkin/devel -DCMAKE_INSTALL_PREFIX=/home/tseng/workspace/catkin/install -G Unix Makefiles" in "/home/tseng/workspace/catkin/build"
####
-- Using CATKIN_DEVEL_PREFIX: /home/tseng/workspace/catkin/devel
-- Using CMAKE_PREFIX_PATH: /home/tseng/workspace/catkin/devel;/opt/ros/noetic
-- This workspace overlays: /home/tseng/workspace/catkin/devel;/opt/ros/noetic
-- Found PythonInterp: /usr/bin/python3 (found suitable version "3.8.10", minimum required is "3") 
-- Using PYTHON_EXECUTABLE: /usr/bin/python3
-- Using Debian Python package layout
-- Using empy: /usr/lib/python3/dist-packages/em.py
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /home/tseng/workspace/catkin/build/test_results
-- Forcing gtest/gmock from source, though one was otherwise available.
-- Found gtest sources under '/usr/src/googletest': gtests will be built
-- Found gmock sources under '/usr/src/googletest': gmock will be built
-- Found PythonInterp: /usr/bin/python3 (found version "3.8.10") 
-- Using Python nosetests: /usr/bin/nosetests3
-- catkin 0.8.10
-- BUILD_SHARED_LIBS is on
-- BUILD_SHARED_LIBS is on
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- ~~  traversing 17 packages in topological order:
-- ~~  - navigation (metapackage)
-- ~~  - map_server
-- ~~  - hybrid_astar
-- ~~  - amcl
-- ~~  - fake_localization
-- ~~  - voxel_grid
-- ~~  - costmap_2d
-- ~~  - nav_core
-- ~~  - base_local_planner
-- ~~  - carrot_planner
-- ~~  - clear_costmap_recovery
-- ~~  - dwa_local_planner
-- ~~  - move_slow_and_clear
-- ~~  - navfn
-- ~~  - global_planner
-- ~~  - rotate_recovery
-- ~~  - move_base
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- +++ processing catkin metapackage: 'navigation'
-- ==> add_subdirectory(navigation/navigation)
-- +++ processing catkin package: 'map_server'
-- ==> add_subdirectory(navigation/map_server)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- Found Bullet: /usr/lib/x86_64-linux-gnu/libBulletDynamics.so  
CMake Error at /usr/share/cmake-3.16/Modules/FindPackageHandleStandardArgs.cmake:146 (message):
  Could NOT find SDL (missing: SDL_LIBRARY SDL_INCLUDE_DIR)
Call Stack (most recent call first):
  /usr/share/cmake-3.16/Modules/FindPackageHandleStandardArgs.cmake:393 (_FPHSA_FAILURE_MESSAGE)
  /usr/share/cmake-3.16/Modules/FindSDL.cmake:188 (FIND_PACKAGE_HANDLE_STANDARD_ARGS)
  navigation/map_server/CMakeLists.txt:12 (find_package)


-- Configuring incomplete, errors occurred!
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeOutput.log".
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeError.log".

解决办法:
$ sudo apt-get install libsdl-dev
$ sudo apt-get install libsdl-image1.2-devgit clone https://github.com/ros-planning/navigation

$ catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
Base path: /home/tseng/workspace/catkin
Source space: /home/tseng/workspace/catkin/src
Build space: /home/tseng/workspace/catkin/build
Devel space: /home/tseng/workspace/catkin/devel
Install space: /home/tseng/workspace/catkin/install
####
#### Running command: "make cmake_check_build_system" in "/home/tseng/workspace/catkin/build"
####
-- Using CATKIN_DEVEL_PREFIX: /home/tseng/workspace/catkin/devel
-- Using CMAKE_PREFIX_PATH: /home/tseng/workspace/catkin/devel;/opt/ros/noetic
-- This workspace overlays: /home/tseng/workspace/catkin/devel;/opt/ros/noetic
-- Found PythonInterp: /usr/bin/python3 (found suitable version "3.8.10", minimum required is "3") 
-- Using PYTHON_EXECUTABLE: /usr/bin/python3
-- Using Debian Python package layout
-- Using empy: /usr/lib/python3/dist-packages/em.py
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /home/tseng/workspace/catkin/build/test_results
-- Forcing gtest/gmock from source, though one was otherwise available.
-- Found gtest sources under '/usr/src/googletest': gtests will be built
-- Found gmock sources under '/usr/src/googletest': gmock will be built
-- Found PythonInterp: /usr/bin/python3 (found version "3.8.10") 
-- Using Python nosetests: /usr/bin/nosetests3
-- catkin 0.8.10
-- BUILD_SHARED_LIBS is on
-- BUILD_SHARED_LIBS is on
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- ~~  traversing 17 packages in topological order:
-- ~~  - navigation (metapackage)
-- ~~  - map_server
-- ~~  - hybrid_astar
-- ~~  - amcl
-- ~~  - fake_localization
-- ~~  - voxel_grid
-- ~~  - costmap_2d
-- ~~  - nav_core
-- ~~  - base_local_planner
-- ~~  - carrot_planner
-- ~~  - clear_costmap_recovery
-- ~~  - dwa_local_planner
-- ~~  - move_slow_and_clear
-- ~~  - navfn
-- ~~  - global_planner
-- ~~  - rotate_recovery
-- ~~  - move_base
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- +++ processing catkin metapackage: 'navigation'
-- ==> add_subdirectory(navigation/navigation)
-- +++ processing catkin package: 'map_server'
-- ==> add_subdirectory(navigation/map_server)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- Found SDL_image: /usr/lib/x86_64-linux-gnu/libSDL_image.so (found version "1.2.12") 
-- Found Boost: /usr/lib/x86_64-linux-gnu/cmake/Boost-1.71.0/BoostConfig.cmake (found version "1.71.0") found components: filesystem 
-- Found PkgConfig: /usr/bin/pkg-config (found version "0.29.1") 
-- +++ processing catkin package: 'hybrid_astar'
-- ==> add_subdirectory(path_planner)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- +++ processing catkin package: 'amcl'
-- ==> add_subdirectory(navigation/amcl)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- Found Boost: /usr/lib/x86_64-linux-gnu/cmake/Boost-1.71.0/BoostConfig.cmake (found version "1.71.0")  
-- Looking for unistd.h
-- Looking for unistd.h - found
-- Looking for drand48
-- Looking for drand48 - found
-- +++ processing catkin package: 'fake_localization'
-- ==> add_subdirectory(navigation/fake_localization)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- +++ processing catkin package: 'voxel_grid'
-- ==> add_subdirectory(navigation/voxel_grid)
-- Looking for sys/time.h
-- Looking for sys/time.h - found
-- +++ processing catkin package: 'costmap_2d'
-- ==> add_subdirectory(navigation/costmap_2d)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- Could NOT find tf2_sensor_msgs (missing: tf2_sensor_msgs_DIR)
-- Could not find the required component 'tf2_sensor_msgs'. The following CMake error indicates that you either need to install the package with the same name or change your environment so that it can be found.
CMake Error at /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
  Could not find a package configuration file provided by "tf2_sensor_msgs"
  with any of the following names:

    tf2_sensor_msgsConfig.cmake
    tf2_sensor_msgs-config.cmake

  Add the installation prefix of "tf2_sensor_msgs" to CMAKE_PREFIX_PATH or
  set "tf2_sensor_msgs_DIR" to a directory containing one of the above files.
  If "tf2_sensor_msgs" provides a separate development package or SDK, be
  sure it has been installed.
Call Stack (most recent call first):
  navigation/costmap_2d/CMakeLists.txt:4 (find_package)


-- Configuring incomplete, errors occurred!
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeOutput.log".
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeError.log".
make: *** [Makefile:992: cmake_check_build_system] Error 1

解决办法:
$ sudo apt-get install ros-noetic-tf2-sensor-msgs

-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- Could NOT find move_base_msgs (missing: move_base_msgs_DIR)
-- Could not find the required component 'move_base_msgs'. The following CMake error indicates that you either need to install the package with the same name or change your environment so that it can be found.
CMake Error at /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
  Could not find a package configuration file provided by "move_base_msgs"
  with any of the following names:

    move_base_msgsConfig.cmake
    move_base_msgs-config.cmake

  Add the installation prefix of "move_base_msgs" to CMAKE_PREFIX_PATH or set
  "move_base_msgs_DIR" to a directory containing one of the above files.  If
  "move_base_msgs" provides a separate development package or SDK, be sure it
  has been installed.
Call Stack (most recent call first):
  navigation/move_base/CMakeLists.txt:4 (find_package)


-- Configuring incomplete, errors occurred!
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeOutput.log".
See also "/home/tseng/workspace/catkin/build/CMakeFiles/CMakeError.log".
make: *** [Makefile:992: cmake_check_build_system] Error 1
Invoking "make cmake_check_build_system" failed

解决办法:
$ sudo apt-get install ros-noetic-move-base-msgs
