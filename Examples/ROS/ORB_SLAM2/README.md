## CHANGES
1.修改ORB_SLAM2源码，更改图片及点云地图显示为彩色，增加自动保存result.pcd

2.**FIX** 运行结束卡死bug

3.**FIX** *Examples/ROS/ORB_SLAM2*编译失败（在*CMakeLists.txt*中加入PCL依赖等即可编译成功）

4.**FIX** PointCloudMapping不完全更新的问题，当发生回环后不能更新校正后的点云地图

5.**ADD** 点云地图PassThrough滤波，去除远处不准确的点

## NOTE
1.编译前需运行：
```bash
	export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/your/path/ORBSLAM2_with_pointcloud_map/ORB_SLAM2_modified/Examples/ROS
```
否则会出错说找不到路径和包

2.运行
```bash
tools/bin_vocabulary
```
生成二进制字典

3.停止运行病保存生成的轨迹与点云地图，请运行
```bash 
rostopic pub /RGBD/cmd std_msgs/String "data: 'stop'"
```

## How To Build

1. ```export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/your/path/ORBSLAM2_with_pointcloud_map/ORB_SLAM2_modified/Examples/ROS```

2. ```mkdir build```

3. ```cmake ..```
 
4. ```make -j4```

## How To Run

1. ```rosbag play -r 1.0 *.bag```
  或使用Kinect
  
2. ```./RGBD ../../../Vocabulary/ORBvoc.bin kinect2_121717234447.yaml```

3. ```rostopic pub /RGBD/cmd std_msgs/String "data: 'stop'"``` 停止建图

4. ```pcl_viewer result.pcd```查看pcd文件