# Installation
You need to have a installed and running docker environment and be a member of the `docker` group.

1. Get this repo
```
git clone https://github.com/meier-rene/MSConvertGUI-docker
cd MSConvertGUI-docker
```

2. Create the container image
```
docker build --rm -t msconvertgui .
```
3. Allow local X11 connections from root
```
xhost +local:root
```
4. Run the container
```
docker run --rm -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v $HOME:/data:rw msconvertgui
```
Substitute `$HOME` with the directory which holds your data. The directory is mounted at /data in your container, which is accessible as Z:\data in MSConvertGUI.
