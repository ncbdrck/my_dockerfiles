This repo contains Dockerfiles that will start from the **Nvidia/CUDAGL** image and automatically install ROS Noetic and all the packages to perform OpenAI with ROS.

- **dockerfile_nvidia_ros** contains a clean installation of CUDA with ROS noetic, Pytorch/Tensorflow and vnc support for visualization
- **dockerfile_rl_ros** contains nvidia_ros with other packages for rl research

To create the Docker Images, execute the following code. 

```
cd 
git clone -b sep2022 https://github.com/ncbdrck/my_dockerfiles.git
cd my_dockerfiles/ 
docker build -f dockerfile_nvidia_ros_sep2022 -t nvidia_ros_11.4 .
docker build -f dockerfile_rl_ros -t rl_ros .
```

To create a Docker Container

```
docker run --name jay-rl-SEP-2022 -itd -v ~/tmp:/mytmp -p 5995:5995 --gpus all rl_ros
docker exec -ti jay-rl-SEP-2022 bash

export DISPLAY=:95
Xvfb $DISPLAY -screen 0 1920x1080x16 &
x11vnc -passwd 1234 -display $DISPLAY -N -forever &
metacity &
```
