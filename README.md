# clairvoyance
ros+opencv demo

本代码库的目的是提供ROS环境下的图像处理演示程序。
图像的来源为笔记本自带的摄像头，在学习ROS + opencv做图像处理的初期你可以先使用笔记本自带的摄像头来熟悉程序运行的整个流程。熟悉后，可以使用硬件来搭建整个系统，比如使用树莓派+摄像头。

本代码库中的程序在ubuntu 16.04LIS中测试通过，使用的ros版本为Kinetic。

一、安装

    1.安装ROS
        官方安装教程：http://wiki.ros.org/kinetic/Installation/Ubuntu
        如果是在笔记本中安装，建议安装ros-kinetic-desktop-full。
        
    2.安装笔记本前置摄像头驱动
        $ sudo apt-get install ros-kinetic-uvc-camera
        $ source /opt/ros/kinetic/setup.bash

    3.下载clairvoyance
        创建工作区
        $ mkdir -p ~/src/clairvoyance_ws/src
        $ cd ~/src/clairvoyance_ws/src
        下载程序
        $ git clone git@github.com:BreederBai/clairvoyance.git
        编译
        $ cd ~/src/clairvoyance_ws
        $ catkin_make
        如果没有遇到报错，恭喜你，编译通过了。
二、运行

    1.启动ROS核心
        打开一个新终端输入
        $ roscore
        
    2.打开笔记本前置摄像头
        $ rosrun uvc_camera uvc_camera_node
    
    3.运行边缘演示程序
        $ cd ~/src/clairvoyance_ws
        $ source devel/setup.bash
        $ rosrun clairvoyance edge_detector
        
    3.运行人脸检测演示程序
        $ cd ~/src/clairvoyance_ws
        $ source devel/setup.bash
        $ rosrun clairvoyance face_detector
        查看原始图像
        rosrun image_view image_view image:=/image_raw
        运行人脸检测程序时需要注意，face_detector文件夹下的haarcascade_frontalface_alt.xml文件。在face_detector.cpp第110行中，需要将face_cascade后的路径替换成你自己的路径。重新编译后，再次运行。
三、常用命令

    1.查看发布的ros主题
        $ rostopic list
