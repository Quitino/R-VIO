# R-VIO

[泡泡机器人推荐词](https://mp.weixin.qq.com/s?__biz=MzI5MTM1MTQwMw==&mid=2247507341&idx=2&sn=0256b30772fe95bc7d98bf61dbf7f1a8&chksm=ec136389db64ea9f8f56d8d97b6e625cdda209fb605398dfa2d9f5177f140cfaecc959818e70&mpshare=1&scene=1&srcid=0814qJcuD2VFBKnFwfYN9d9j&sharer_sharetime=1565766351017&sharer_shareid=662e33bcf39b24da66575a9f1c3f9ab8&pass_ticket=F%2FDcQUFoziFQRIZO5nFqbGSWQROwfTXyyFj%2B3FTug77yGQBpxqgMTzUTPyXdfXYW#rd)

R-VIO is an efficient, lightweight, **robocentric visual-inertial odometry** algorithm for consistent 3D motion tracking using only a monocular camera and a 6-axis IMU. Different from standard world-centric VINS algorithms which directly estimate absolute motion of the sensing platform with respect to a fixed, gravity-aligned, global frame of reference, R-VIO estimates the relative motion of higher accuracy with respect to a moving local frame (for example, IMU frame) and updates the global pose (orientation and position) estimate through composition. This algorithm is developed with the robocentric sliding-window filtering-based VIO framework that we originally proposed in our *IROS2018* paper and further extended in our recent *IJRR* paper:

- Zheng Huai and Guoquan Huang, **Robocentric visual-inertial odometry**, *The International Journal of Robotics Research (IJRR)*, July 2019: [here](https://journals.sagepub.com/doi/10.1177/0278364919853361).

- Zheng Huai and Guoquan Huang, **Robocentric visual-inertial odometry**, *IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)*, Madrid, Spain, Oct 1-5, 2018: [here](https://ieeexplore.ieee.org/document/8593643).

Video (on **EuRoC** and our handheld datasets): https://www.youtube.com/watch?v=UtiZ0EKa55M.
![](https://media.giphy.com/media/RMecOYlfxEcy4T8JdS/giphy.gif)

Video (on our 9.8km **urban driving** dataset): https://www.youtube.com/watch?v=l9IC2ddBEYQ.
![](rvio.gif)

## 1. Prerequisites

We have tested the code under Ubuntu **16.04** and ROS **Kinetic**.

### ROS
Download and install instructions can be found at: http://wiki.ros.org/kinetic/Installation/Ubuntu.

Additional ROS packages needed: tf, sensor_msgs, geometry_msgs, nav_msgs, cv_bridge, eigen_conversions.

### Eigen
Download and install instructions can be found at: http://eigen.tuxfamily.org. **Required at least 3.1.0**.

### OpenCV
Download and install instructions can be found at: http://opencv.org. **Required at leat 2.4.3**. **Tested with 2.4.11 and 3.3.1**.

## 2. Build and Run
First, `git clone` the repository and `catkin_make` it. Then, to run `rvio` with single camera/IMU inputs from the ROS topics `/camera/image_raw` and `/imu`, a config file in *config* folder and the corresponding launch file in *launch* folder (for example, `rvio_euroc.yaml` and `euroc.launch` are for [EuRoC](https://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets) dataset) are needed, and to visualize the outputs of R-VIO please use `rviz` with the settings file `rvio_rviz.rviz` in *config* folder.
  ```
  Terminal 1: roscore
  ```
  ```
  Terminal 2: rviz (AND OPEN rvio_rviz.rviz IN THE CONFIG FOLDER)
  ```
  ```
  Terminal 3: roslaunch rvio euroc.launch
  ```
  ```
  Terminal 4: rosbag play --pause V1_01_easy.bag /cam0/image_raw:=/camera/image_raw /imu0:=/imu
  ```
  这一步不要暂停
  ```
  Terminal 4: rosbag play V1_01_easy.bag /cam0/image_raw:=/camera/image_raw /imu0:=/imu
  ```
You can also run R-VIO with your own sensor (data) by creating a config file `rvio_NAME_OF_YOUR_DATA.yaml` in *config* folder and the corresponding launch file `NAME_OF_YOUR_DATA.launch` in *launch* folder referring to the above EuRoC example.

## 3. License

The source code is released under [GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html) license.

We are still working on improving the code reliability. For any technical issue, please contact Zheng Huai: <zhuai@udel.edu>.

For commercial inquiries, please contact Guoquan (Paul) Huang: <ghuang@udel.edu>.

