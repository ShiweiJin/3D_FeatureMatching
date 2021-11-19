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
