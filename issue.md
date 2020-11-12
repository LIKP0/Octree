# Project for implementation of Octree structure and related algorithms in OpenCV

​	We are going to implement an **Octree** structure and some related algorithms such as **Point cloud Compression， K nearest neighbors search** and **Spatial change detection** algorithms in OpenCV.

### Why we do it?

​	It's heard that OpenCV is going to have its 3D part in the future version and we want to do some contributions. The task is meaningful because Octree is a basic structure used in many aspects and it is very powerful. It enables spatial partitioning, downsampling and search operations on the point data set.

### A brief introduction of Octree and related algorithms

#### Octree

​	Octree is a kind of spatial partitioning on 3D dimension with each node representing a cubic space. According to the 3D coordinate system, we can divide the space into 8 Octants. For each octants as a node, it describes a cubic bounding box which encapsulates many points of the database of point cloud file. For root node, it describes a cubic bounding box which encapsulates all points in the point cloud file database. Then for each child node of certain parent node, it respectively represents one part cubic box of the parent cubic box with parent box division of eight equal parts.

![image](https://github.com/LIKP0/Octree/blob/main/other_src/octree.png)

The picture comes from Wikipedia.(https://zh.wikipedia.org/wiki/%E5%85%AB%E5%8F%89%E6%A0%91)

#### Point cloud Compression

​	The point cloud of a certain file is composed of many enormous data sets which is associated with the distance, color, normal vector and other additional information to describe the 3D points. Moreover, the process of creating point cloud is expeditious. Therefore, it requires considerable resource space to store the data sets. Once the point clouds needs to be stored or transferred with speed limited communication channels, point cloud compression will make the process much efficacious. It will be able to encode all kinds of point clouds data like point reference, varying point size, resolution, density and point ordering. And with octree data structure, it can efficiently merge several point cloud data source to compress them.

####  KNN search

​	KNN -- K nearest neighbor algorithm.

​	The mechanism of this algorithm is as follow:

```
Create a priority queue of K length.
Recursively find the child node until reach the tree depth.
Maintain the priority queue of distance between each point in each node and the target point.
```

​	In theory, it needs O(point.count) to get the final queue. However, this algorithm will maintain a distance which is the farthest point relative to the target point in the K heap. And if the center of one cube is farther than the farthest distance in K heap plus the half of the diagonal length (the square root of three times the square of the side length) relative to the target point, it will be discarded. Otherwise, it will be searched ,maintain the K heap and update the distance which is the farthest point relative to the target point in the K heap. This part sufficiently exert the benefits of octree to cut the branch and then promote the execution speed.

#### **Spatial change detection**

​	With octree data structure for organizing three dimensional points, the algorithm can realize detection of spatial changes between several unorganized point clouds data. 

​	Suppose we initiate point cloud 1 with random point data, and generate its corresponding octree structure -- octreeA based on this point cloud. Then initiate point cloud 2 with random point data, and generate its corresponding octree structure -- octreeB based on this point cloud. Then we store and manage two trees in the memory at the same time. The algorithm can implement a memory pool that reuses already allocated node objects. Then we can retrieve the points stored at voxels of the octreeB which do not exist in the octreeA. Now we detect the spatial change successfully.

### About us

​	Our team has three members: ZhiYue Wang@https://github.com/wangihzyue
                              JiaLin Li@https://github.com/LIKP0
                              HaoTian Gao@https://github.com/Jimmy-7664
                              under the guide of Professor YU@. 
  And we should give our especial thanks to **HUAWEI** for external support. We are senior students of Southern university of science and technology. This program is a big project for us in a course called **Innovative practice** lasts for one year and a half. In honest, it is very difficult for us to develop such a huge project without any basic knowledge in 3D field but we will try our best. Finally, **we hope for your support sincerely, come and discuss with us below this issue!**
