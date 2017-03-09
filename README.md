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
Substitute `$HOME` with the directory holding your data. The directory is mounted at /data in your container, which is accessible as Z:\data in MSConvertGUI.


## Testing commandline msconvert.exe (which fails on Thermo RAW data)
This container can be used in a similar way to test the msconvert.exe program. A suitable command would be
```
docker run --rm -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v $HOME:/data:rw \
  msconvertgui /bin/bash -c "cd /data; wine msconvert small.RAW"
```
if your data file `small.RAW` is directly in the exposed folder.

Another option is of course to enter a interactive shell with
```
docker run -ti -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v $HOME::/data:rw \
  msconvertgui /bin/bash
```
and issue a `wine msconvert <data_file>` manually.
