# FROM ros:noetic-ros-core-focal
FROM px4io/px4-dev-ros-noetic:2024-05-18
LABEL maintainer="johntgz@nus.edu.sg"

#####
# Install dependencies
#####

# install bootstrap tools
RUN apt-get update && apt-get install --no-install-recommends -y \
    vim \
    tmux \
    && rm -rf /var/lib/apt/lists/*

# Copy .bashrc file
COPY .bashrc /root/

#####
# Clone repos
#####
WORKDIR /ros_ws/src/
RUN git clone https://github.com/Temasek-Dynamics/PX4-SITL-Docker.git -b main
WORKDIR /ros_ws/
RUN source /opt/ros/noetic/setup.bash \
    && catkin build 

WORKDIR /
RUN git clone https://github.com/PX4/PX4-Autopilot.git
WORKDIR /PX4-Autopilot
RUN git checkout 2110eae25d32ef102c5e44f2590fd7f9d65fc44d
RUN DONT_RUN=1 make px4_sitl gazebo-classic

#####
# Environment variables
#####
# DRONE_ID environment variable can be overriden on docker image startup
ENV DRONE_ID=0

ENV ROS_DISTRO=noetic

# Enable the use of `source` keyword
SHELL ["/bin/bash", "-c"] 

COPY ./ros_entrypoint.sh /
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
