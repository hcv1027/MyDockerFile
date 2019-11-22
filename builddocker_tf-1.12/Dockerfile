# FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
# e.g. FROM osrf/ros:kinetic-desktop-full
FROM tensorflow/tensorflow:1.12.3-gpu-py3

RUN apt-get -y update && \
  apt-get -y install vim lsb-release

# optional, if the default user is not "root",
# you might need to switch to root here and at the end of the script to the original user again.
# e.g.
USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
  pkg-config \
  libxau-dev \
  libxdmcp-dev \
  libxcb1-dev \
  libxext-dev \
  libx11-dev && \
  rm -rf /var/lib/apt/lists/*

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
COPY --from=nvidia/opengl:1.0-glvnd-runtime-ubuntu16.04 \
  /usr/local/lib/x86_64-linux-gnu \
  /usr/local/lib/x86_64-linux-gnu

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
COPY --from=nvidia/opengl:1.0-glvnd-runtime-ubuntu16.04 \
  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json \
  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json

RUN echo '/usr/local/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
  ldconfig && \
  echo '/usr/local/$LIB/libGL.so.1' >> /etc/ld.so.preload && \
  echo '/usr/local/$LIB/libEGL.so.1' >> /etc/ld.so.preload

RUN apt-get update && apt-get install -y --no-install-recommends python-qt4 libxcursor-dev libxrandr-dev && rm -rf /var/lib/apt/lists/*
RUN apt install -y netbase && rm -rf /var/lib/apt/lists/*
RUN pip install jupyter numpy scipy h5py eventlet flask-socketio seaborn pandas ffmpeg imageio moviepy opencv-python requests moviepy

# Term 1 workdir
RUN mkdir /src
WORKDIR "/src"

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
  ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
  ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics


# TensorBoard
EXPOSE 6006
# Jupyter
EXPOSE 8888
# Flask Server
EXPOSE 4567

# setup entrypoint
CMD /bin/bash

# Build command
# docker build --build-arg user_pass=josper_pass --tag ubuntu:16.04-josper .
