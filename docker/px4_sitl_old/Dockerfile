# FROM ros:noetic-ros-core-focal
FROM gestelt/px4_sitl_gz:base
LABEL maintainer="johntgz@nus.edu.sg"

#####
# Environment variables
#####



# Enable the use of `source` keyword
SHELL ["/bin/bash", "-c"] 

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
