This repo contains Dockerfiles that will start from the **Nvidia/CUDAGL** image and automatically install ros and all the packages to perform OpenAI with ROS.

- **dockerfile_nvidia_ros** contains clean installation of CUDA with ROS noetic
- **dockerfile_openai_ros** contains nvidia_ros with openai_ros framework with Pytorch/Tensorflow
- **dockerfile_openai_ros_sim** contains openai_testv2 with fecth and iri_wam simulation
- **dockerfile_openai_ros_sim_vnc** contains openai_ros_sim_v1 with vnc support for visualization

To create the Docker Images, execute the following code. 

```
git clone https://github.com/ncbdrck/my_dockerfiles.git
cd my_dockerfiles/ 
docker build -f dockerfile_nvidia_ros -t nvidia_ros .
docker build -f dockerfile_openai_ros -t openai_testv2 .
docker build -f dockerfile_openai_ros_sim -t openai_ros_sim_v1 .
docker build -f dockerfile_openai_ros_sim_vnc -t openai_ros_sim_vnc_v1 .
```
