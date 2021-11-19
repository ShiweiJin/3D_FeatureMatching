# 3D_FeatureMatching

# Ubuntu PCL
This document will record some problems during the PCL installation.

1. Uninstall PCL

```sudo rm -r /usr/include/pcl-1.8 /usr/share/pcl-1.8 /usr/bin/pcl* /usr/lib/libpcl*```


2. sudo apt-get update failed
https://blog.csdn.net/github_39533414/article/details/89068736

I open the /etc/apt path. And I can find there is a folder called sources.list.d. And we can compare the files names which are all the same as the errors show in the terminal. So I delete the error files and apt-get update works well again.

3. 
