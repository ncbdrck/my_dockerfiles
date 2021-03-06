This repo contains Dockerfiles that will start from the **Nvidia/CUDAGL** image and automatically install ROS Noetic and all the packages to perform OpenAI with ROS.

- **dockerfile_nvidia_ros** contains a clean installation of CUDA with ROS noetic
- **dockerfile_openai_ros** contains nvidia_ros with openai_ros framework with Pytorch/Tensorflow
- **dockerfile_openai_ros_sim** contains openai_ros with fecth and iri_wam simulation
- **dockerfile_openai_ros_sim_vnc** contains openai_ros_ simulations with vnc support for visualization

To create the Docker Images, execute the following code. 

```
git clone https://github.com/ncbdrck/my_dockerfiles.git
cd my_dockerfiles/ 
docker build -f dockerfile_nvidia_ros -t nvidia_ros_11.1 .
docker build -f dockerfile_openai_ros -t openai_ros .
docker build -f dockerfile_openai_ros_sim -t openai_ros_sim .
docker build -f dockerfile_openai_ros_sim_vnc -t openai_ros_sim_vnc .
```

To create a Docker Container

```
docker run --name my-openai-v1 -it -v ~/tmp:/mytmp -p 5910:5910 --gpus all openai_ros_sim_v1
```
