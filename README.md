# NOTE
Based on [gaoxiang12/ORBSLAM2_with_pointcloud_map](https://github.com/gaoxiang12/ORBSLAM2_with_pointcloud_map.git)


# ORBSLAM2_with_pointcloud_map
This is a modified ORB_SLAM2 (from https://github.com/raulmur/ORB_SLAM2, thanks for Raul's great work!) with a online point cloud map module running in RGB-D mode. You can visualize your point cloud map during the SLAM process. 

# How to Install
Unzip the file you will find two directories. First compile the modified g2o:

```
  cd g2o_with_orbslam2
  mkdir build
  cd build
  cmake ..
  make 
```

Following the instructions from the original g2o library: [https://github.com/RainerKuemmerle/g2o] if you have dependency problems. I just add the extra vertecies and edges provided in ORB_SLAM2 into g2o. 

Then compile the ORB_SLAM2. You need firstly to compile the DBoW2 in ORB_SLAM2_modified/Thirdpary, and then the Pangolin module (https://github.com/stevenlovegrove/Pangolin). Finally, build ORB_SLAM2:

```
cd ORB_SLAM2_modified
mkdir build
cd build
cmake ..
make
```

To run the program you also need to download the ORB vocabulary (which is a large file so I don't upload it) in the original ORB_SLAM2 repository.

# Run examples
Prepare a RGBD camera or dataset, give the correct parameters and you can get a ORB SLAM with point cloud maps like the example.jpg in this repo.

# CHANGES
1.修改ORB_SLAM2源码，更改图片及点云地图显示为彩色，增加自动保存result.pcd

2.**FIX** 运行结束卡死bug

3.**FIX** *Examples/ROS/ORB_SLAM2*编译失败（在*CMakeLists.txt*中加入PCL依赖等即可编译成功）

4.**FIX** PointCloudMapping不完全更新的问题，当发生回环后不能更新校正后的点云地图

5.**ADD** 点云地图PassThrough滤波，去除远处不准确的点

**Run It In ROS [README](./Examples/ROS/ORB_SLAM2/README.md)**