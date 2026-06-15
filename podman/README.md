# Create software image
```
podman pull docker.io/osrf/ros:jazzy-desktop-full
podman run -it --rm --name rko_lio docker.io/osrf/ros:jazzy-desktop-full
```

```
   apt update && apt -y upgrade
   apt install ros-$ROS_DISTRO-rko-lio
```

```
podman commit rko_lio ghcr.io/ecervera/rko_lio:latest
podman push ghcr.io/ecervera/rko_lio:latest
```

# Run container

```
xhost +local:$USER
podman run -it --rm --name rko_lio \
    --env="DISPLAY=$DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --device /dev/dri \
    ghcr.io/ecervera/rko_lio:latest
```
