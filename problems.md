# Problems when building this package
## Prerequisite
- [ros2 installation](https://index.ros.org/doc/ros2/Installation/#installationguide)
- [rosdep installation](https://wiki.ros.org/rosdep#Installing_rosdep)
- [colcon installation](https://index.ros.org/doc/ros2/Tutorials/Colcon-Tutorial/#colcon)
- [git installation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
## Complete process
```
# 1. ssh进入ubuntu@192.168.11.45
ssh ubuntu@192.168.11.45
# 2. 创建ROS2 Foxy workspace
source /opt/ros/foxy/setup.bash
mkdir -p ~/ros2_ws/src
# 3. clone源码
cd ~/ros2_ws/src
git clone https://github.com/2quarius/rplidar_ros.git -b ros2-wheeltec-rplidar
# 4. 下载依赖
cd ~/ros2_ws
rosdep install -i --from-path src --rosdistro foxy -y
# 5. colcon build
cd ~/ros2_ws
colcon build --symlink-install --packages-select rplidar_ros
# Finished <<< rplidar_ros
# 完成！
```
接下来是运行
```
ros2 launch rplidar_ros rplidar<.version>.launch.py
```
## `rosdep`没有下载任何依赖
- 原因：环境变量`AMENT_PREFIX_PATH`的问题
- cause：因为之前根据官方ros2 installation的教程安装，将`source ~/ros2_foxy/ros2-linux/setup.bash`写入了`~/.bashrc`，后面在创建workspace的时候又将`source /opt/ros/foxy/setup.bash`写入了`~/.bashrc`，`AMENT_PREFIX_PATH`被设置为`/opt/ros/foxy:/home/ubuntu/ros2_foxy/ros2-linux`。因此之后package所需的依赖都在`AMENT_PREFIX_PATH`下寻找，没有的话才会去下载。而如果将`AMENT_PREFIX_PATH`修改为`/opt/ros/foxy`，再次运行rosdep install去安装官方turtlesim时会下载和`home/ubuntu/ros2_foxy/ros2-linux`里重复的依赖。
## `colcon build`没有`--packages-selection`选项
solution:
```bash
sudo apt install python3-colcon-package-selection
```
## `colcon build`找不到package
solution:
```bash
sudo apt install python3-colcon-ros
```

