# Update for unpacked ROB_SLAM with pcl view repo

## build:

### build the whole project ( inclouding binary loading tools ):

Before all the cmd, **DONOT** forget to download the Vocabulary form the [origin repo](https://github.com/raulmur/ORB_SLAM2) and place it into dir ./Vocabulary

```bash
     chmod +x build.sh
     ./build.sh
```

### only build the ORB_SLAM2 mode with pcl

```bash
    mkdir build
    cd build
    cmake ..
    make -j
```

## Run:

```bash
    ./run/rgbd_tum Vocabulary/ORBvoc.bin path_to_settings path_to_sequence path_to_association
```

# What are modified:

* adding a pointcloud viewer with loopclosing ( realized by adding a viewer thread )

点云更新思路： 插入关键帧时，同时生成一个pointcloud帧，该帧中保存了ID、对应的点云，以及点云变换矩阵。当检测到回环时，关键帧被更新，此时，获取所有更新后的关键帧的位姿，更新pointcloud帧对应ID的点云变换矩阵，从而根据跟新后的点云变换矩阵得到新的点云地图，替换老的点云地图。
通过在8m*8m的房间进行RGBD建图实验，存在一个全局回环的情况下，更新点云与不更新点云得到的结果无明显差别？？？

