# FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
# e.g. FROM osrf/ros:kinetic-desktop-full
FROM nvidia/opengl:1.2-glvnd-runtime-ubuntu18.04

RUN apt -y update && \
  apt -y --no-install-recommends install vim lsb-release curl unzip git software-properties-common bash-completion && \
  rm -rf /var/lib/apt/lists/*

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
  ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
  ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics
