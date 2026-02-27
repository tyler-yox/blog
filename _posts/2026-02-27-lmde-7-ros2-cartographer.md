---
layout: post
title: Installing Cartographer in ROS2 From Source in LMDE 7
tags: ros lmde mint debian
categories: computing
---
## Clone ros2 forks of Cartographer
```
git clone https://github.com/ros2/cartographer.git
cd cartographer
git remote add cartographer_ros https://github.com/ros2/cartographer_ros.git
git fetch cartographer_ros
git merge cartographer_ros/ros2 -s ours --allow-unrelated-histories
```
## Install Abseil
```
sudo apt install ninja-build stow libboost-iostreams-dev libceres-dev liblua5.4-dev protobuf-compiler -y
cd scripts
./install_abseil.sh
```

The following modifications were needed to compile and link with Abseil 
- abseil-cpp/absl/synchronization/internal/graphcycles.cc
    - add #include <limits>
- abseil-cpp/absl/strings/internal/str_format/extension.h
    - add #include <cstdint>
- abseil-cpp/absl/debugging/failure_signal_handler.cc
    - add <size_t> to this line:
        - modify size_t stack_size = (std::max<size_t>(SIGSTKSZ, 65536) + page_mask) & ~page_mask
- abseil-cpp/absl/base/config.h
    - delete #define ABSL_HAVE_STD_STRING_VIEW 1

```
cd abseil-cpp/build
ninja
sudo ninja install
cd /usr/local/stow
sudo stow absl
cd -
```
## Build Cartographer
```
colcon build --cmake-args -G Ninja
```
