# OpenCV 2.x Dockerfile for development
## Building
To build the image just run:

```bash
$ docker build . -t <image-name>
```
## Running container
To run it you have to adjust the permission to the X server host. So run the following command in the docker host machine:

```bash
$ xhost +local:root
```

This is a lazy workaround to permit connection from the container, and it can be improved as explained [here](http://wiki.ros.org/docker/Tutorials/GUI).

After that you can run your docker container:

```bash
$ docker run -it \
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --volume="<local-dev-dir>:/root" \
    --device /dev/video0 \
    <image-name>
```
Note that we map the host camera divice to be used by docker container.

When you finish, disable permission to connect to your X server host:

```bash
$ xhost -local:root
```
