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

or

cd nvidia/
docker build -f dockerfile_nvidia_ros_sep2022_v2 -t nvidia_ros_11.2.2 .
docker build -f dockerfile_rl_ros_v2 -t rl2_ros .

or
cd tensorflow/
docker build -f dockerfile_tensor_ros -t tensor_ros_noetic .

```

To create a Docker Container

```
docker run --name jay-rl-SEP-2022 -itd -v ~/tmp:/mytmp -p 5995:5995 --gpus all rl_ros
docker exec -ti jay-rl-SEP-2022 bash

export DISPLAY=:95
Xvfb $DISPLAY -screen 0 1920x1080x16 &
x11vnc -passwd 1234 -display $DISPLAY -N -forever &
metacity &


for the second v2

docker run --name jay-rl2-SEP-2022 -itd -v ~/tmp:/mytmp -p 5997:5997 --gpus all rl2_ros
docker exec -ti jay-rl2-SEP-2022 bash

export DISPLAY=:97
Xvfb $DISPLAY -screen 0 1920x1080x16 &
x11vnc -passwd 1234 -display $DISPLAY -N -forever &
metacity &


```

leftover
```
# Simulations
RUN source /opt/ros/noetic/setup.bash \
 && mkdir -p ~/simulation_ws/src \
 && cd ~/simulation_ws/ \
 && catkin_make \
 && source devel/setup.bash

RUN echo "source ~/simulation_ws/devel/setup.bash" >> ~/.bashrc
RUN source ~/.bashrc

# Create a Catkin workspace
RUN source /opt/ros/noetic/setup.bash \
 && mkdir -p ~/catkin_ws/src \
 && cd ~/catkin_ws/ \
 && catkin_make \
 && source devel/setup.bash

RUN echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
RUN source ~/.bashrc

# Install openai_ros
RUN cd ~/catkin_ws/src \
 && git clone -b kinetic-devel https://github.com/ncbdrck/openai_ros.git \
 && git clone https://ncbdrck@bitbucket.org/theconstructcore/theconstruct_msgs.git \
 && cd ~/catkin_ws \
 && rosdep install --from-paths src --ignore-src -r -y

RUN cd ~/catkin_ws \
 && source devel/setup.bash \
 && catkin_make \
 && source devel/setup.bash
 
# Install Fetch robot
RUN source /opt/ros/noetic/setup.bash \
 && cd ~/catkin_ws/src \
 && git clone -b noetic https://ncbdrck@bitbucket.org/theconstructcore/fetch_tc.git \
 && git clone https://ncbdrck@bitbucket.org/theconstructcore/spawn_robot_tools.git \
 && git clone https://github.com/mikeferguson/simple_grasping.git \
 && cd ~/catkin_ws \
 && rosdep install --from-paths src --ignore-src -r -y

RUN cd ~/catkin_ws \
 && source devel/setup.bash \
 && catkin_make \
 && source devel/setup.bash
 
# Install iri_wam robot
RUN source /opt/ros/noetic/setup.bash \
 && cd ~/catkin_ws/src \
 && git clone -b noetic https://ncbdrck@bitbucket.org/theconstructcore/iri_wam.git \
 && git clone https://ncbdrck@bitbucket.org/theconstructcore/hokuyo_model.git \
 && cd ~/catkin_ws \
 && rosdep install --from-paths src --ignore-src -r -y

RUN cd ~/catkin_ws \
 && source devel/setup.bash \
 && catkin_make \
 && source devel/setup.bash


```
