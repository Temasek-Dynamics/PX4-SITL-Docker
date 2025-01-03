# PX4-SITL-Docker
A PX4-SITL docker image instance. Intended for testing Mavlink communications with MavROS on ROS2

## Dependencies
1. [Docker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

## Build and run PX4 SITL instance
```bash
# All-in-one build and push (add --no-cache for a clean rebuild)
docker build -t gestelt/px4_sitl_gz:latest .

# xhost + Specifies that access is unlimited. Access control is turned off.
xhost +
docker run -it --privileged \
            --env=LOCAL_USER_ID="$(id -u)" \
            -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
            -e DISPLAY=:0 \
            --network host \
            --name=px4_sim gestelt/px4_sitl_gz:latest bash
            # --rm \
            # -p 14560:14570/udp \
docker run -it --privileged --network host --rm gestelt/px4_sitl_gz:latest
```

## Enter existing container
```bash
# Start stopped container
docker start <container_id>
# Start additional bash sessions in same container
docker exec -it <container_id> bash
```

## Save containers as new images
```bash
# List all docker containers
docker ps -a
# Commit changes
docker commit CONTAINER_NAME gestelt/px4_sitl_gz:latest
# push 
docker push gestelt/px4_sitl_gz:latest
# Inspect the container
docker container inspect CONTAINER_NAME
```

