# FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
# e.g. FROM osrf/ros:kinetic-desktop-full
FROM tensorflow/tensorflow:1.15.0-gpu-py3-jupyter

RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  vim \
  lsb-release \
  unzip \
  git && \
  rm -rf /var/lib/apt/lists/*

# optional, if the default user is not "root",
# you might need to switch to root here and at the end of the script to the original user again.
# e.g.
USER root

# Base
RUN dpkg --add-architecture i386 && \
  apt-get update && apt-get install -y --no-install-recommends \
  libxau6 libxau6:i386 \
  libxdmcp6 libxdmcp6:i386 \
  libxcb1 libxcb1:i386 \
  libxext6 libxext6:i386 \
  libx11-6 libx11-6:i386 && \
  rm -rf /var/lib/apt/lists/*

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
  ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
  ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics,compat32,utility

RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
  echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

# Required for non-glvnd setups.
ENV LD_LIBRARY_PATH /usr/lib/x86_64-linux-gnu:/usr/lib/i386-linux-gnu${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}:/usr/local/nvidia/lib:/usr/local/nvidia/lib64

# Runtime
RUN apt-get update && apt-get install -y --no-install-recommends \
  libglvnd0 libglvnd0:i386 \
  libgl1 libgl1:i386 \
  libglx0 libglx0:i386 \
  libegl1 libegl1:i386 \
  libgles2 libgles2:i386 && \
  rm -rf /var/lib/apt/lists/*

COPY 10_nvidia.json /usr/share/glvnd/egl_vendor.d/10_nvidia.json

# Devel
RUN apt-get update && apt-get install -y --no-install-recommends \
  pkg-config \
  libglvnd-dev libglvnd-dev:i386 \
  libgl1-mesa-dev libgl1-mesa-dev:i386 \
  libegl1-mesa-dev libegl1-mesa-dev:i386 \
  libgles2-mesa-dev libgles2-mesa-dev:i386 && \
  rm -rf /var/lib/apt/lists/*

# Term 1 workdir
RUN mkdir /src
WORKDIR "/src"

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
