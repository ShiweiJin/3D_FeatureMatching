# Ubuntu PCL
This document will record some problems during the PCL installation.

### 1. Uninstall PCL

```sudo rm -r /usr/include/pcl-1.8 /usr/share/pcl-1.8 /usr/bin/pcl* /usr/lib/libpcl*```


### 2. sudo apt-get update failed
https://blog.csdn.net/github_39533414/article/details/89068736
![image](https://user-images.githubusercontent.com/47040892/142699365-cbe1bef6-917c-48e9-af4f-b4bb82904fdd.png)

I open the /etc/apt path. And I can find there is a folder called sources.list.d. And we can compare the files names which are all the same as the errors show in the terminal. So I delete the error files and apt-get update works well again.

### 3. PCL Install
Reference: Install PCL 1.8.0 on Ubuntu 16.04
Ubuntu 18.04 PCL 1.11.0 install.sh

```bash
# Clone latest PCL
sudo apt-get update
sudo apt-get install git

cd ~/Documents
git clone https://github.com/PointCloudLibrary/pcl.git pcl-trunk
ln -s pcl-trunk pcl
cd pcl

# Install prerequisites
sudo apt-get install g++
sudo apt-get install cmake cmake-gui
sudo apt-get install doxygen
sudo apt-get install mpi-default-dev openmpi-bin openmpi-common
sudo apt-get install libflann1.9 libflann-dev
sudo apt-get install libeigen3-dev
sudo apt-get install libboost-all-dev
sudo apt-get install libvtk6-dev libvtk6.3 libvtk6.3-qt
sudo apt-get install 'libqhull*'
sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev
sudo apt-get install libgtest-dev
sudo apt-get install git-core freeglut3-dev pkg-config
sudo apt-get install build-essential libxmu-dev libxi-dev
sudo apt-get install libusb-1.0-0-dev graphviz mono-complete
sudo apt-get install libqt4-dev openjdk-11-jdk openjdk-11-jre 
# sudo apt-get install qt-sdk openjdk-9-jdk openjdk-9-jre
sudo apt-get install phonon-backend-gstreamer
sudo apt-get install phonon-backend-vlc
sudo apt-get install libopenni-dev libopenni2-dev
```

During the package installation, there will exist some problems like cannot find the packages, which means the wrong package version is specified. Usually, the terminal will remind you which version is fit for your current setup.

During the build and make. There exist some conflicts with anaconda environment packages. Some of them are needed and some of them will cause conflicts. Thus we need to move some files. The detail information is shown in:

https://blog.csdn.net/u014734886/article/details/93029349

该作者使用的是anaconda2，它删除了anaconda2/lib下的libuuid库文件。于是我找到自己anaconda3目录下的lib，搜索libuuid，找到了5个文件

将他们全部删除，再运行make，在一段漫长的等待后，终于成功编译了！

```bash
# Compile and install PCL
mkdir release
cd release
cmake -DCMAKE_BUILD_TYPE=None -DBUILD_GPU=ON -DBUILD_apps=ON -DBUILD_examples=ON ..
make
sudo make install
```

### 4.Test
https://zhuanlan.zhihu.com/p/92164338

Based on the test files created on this website, we can test the PCL is correctly installed or not.

### 5. Cmake status, not the error
https://github.com/PointCloudLibrary/pcl/issues/2487

During the cmake, there will show some information like

```bash
-- Could NOT find OpenNI (missing: OPENNI_LIBRARIES OPENNI_INCLUDE_DIRS) 
CMake Warning at cmake/pcl_targets.cmake:864 (message):
  OpenNI grabber support: not building because OpenNI not found
Call Stack (most recent call first):
  CMakeLists.txt:315 (PCL_ADD_GRABBER_DEPENDENCY)


-- Could NOT find OpenNI2 (missing: OPENNI2_LIBRARIES OPENNI2_INCLUDE_DIRS) 
CMake Warning at cmake/pcl_targets.cmake:864 (message):
  OpenNI2 grabber support: not building because OpenNI2 not found
Call Stack (most recent call first):
  CMakeLists.txt:316 (PCL_ADD_GRABBER_DEPENDENCY)


-- Could NOT find FZAPI (missing: FZAPI_LIBS FZAPI_INCLUDE_DIRS) 
CMake Warning at cmake/pcl_targets.cmake:864 (message):
  Fotonic camera support: not building because FZAPI not found
Call Stack (most recent call first):
  CMakeLists.txt:317 (PCL_ADD_GRABBER_DEPENDENCY)


-- Could NOT find ENSENSO (missing: ENSENSO_LIBRARIES ENSENSO_INCLUDE_DIRS) 
CMake Warning at cmake/pcl_targets.cmake:864 (message):
  IDS-Imaging Ensenso camera support: not building because Ensenso not found
Call Stack (most recent call first):
  CMakeLists.txt:318 (PCL_ADD_GRABBER_DEPENDENCY)
  ```
  
  They are normal. We don't need to respond to these warnings.

### Some other useful Reference
https://blog.csdn.net/yingmai77
