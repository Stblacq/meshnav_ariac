# ariac2019-docker
Has the docker containerisation for [ARIAC2019](https://www.nist.gov/el/intelligent-systems-division-73500/agile-robotics-industrial-automation-competition) 


## Requirements

- This requires the following packages to be installed on the host machine
  - [docker](https://www.docker.com/), can be installed from here https://docs.docker.com/install/linux/docker-ce/ubuntu/
  - `nvidia-docker2`, can be installed from here https://github.com/NVIDIA/nvidia-docker#quickstart

     #### `nvidia-docker2` can be installed on Ubuntu 14.04/16.04/18.04 
    ```sh
    # If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
    docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
    sudo apt-get purge -y nvidia-docker

    # Add the package repositories
    curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
      sudo apt-key add -
     distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
    curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
      sudo tee /etc/apt/sources.list.d/nvidia-docker.list
    sudo apt-get update

    # Install nvidia-docker2 and reload the Docker daemon configuration
    sudo apt-get install -y nvidia-docker2
    sudo pkill -SIGHUP dockerd

    # Test nvidia-smi with the latest official CUDA image
    docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
    ```
- This also requires a directory named `ariac2019_home` in the `/home` directory on host machine, which will be mounted as `/home` directory inside the docker container. This directory holds all the code and files which can be accessed inside the container.

## Quick-start

```sh
# clone this repo
$ git clone https://github.com/sumanth-nirmal/ariac2019-docker.git
$ cd ariac2019-docker
# Start the docker container for ARIAC2019
~/ariac2019-docker$ bash ariac2019_docker.sh start

# Enter the container
~/ariac2019-docker$ bash ariac2019_docker.sh enter

# launch ARIAC2019 sample environment
$ roslaunch osrf_gear sample_environment.launch
```

This should launch the sample environment as shown below:

## Docker file

The repository contains the Dockerfile which is based on `Ubuntu 18.04` with `nvidia-docker2` beta opengl support https://hub.docker.com/r/nvidia/opengl. The Dockerfile contians the following packages 

- [ros-melodic-desktop-full](http://wiki.ros.org/melodic)
- [gazebo9](http://gazebosim.org/)
- ariac3

Also has some utilities like `git`, `git-gui`, `vim`, `htop`, `terminator`, `atom` etc.

### Build Docker image

The docker image can be built locally as below:

```sh
$
```
