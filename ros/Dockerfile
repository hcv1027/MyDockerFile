# FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
# e.g. FROM osrf/ros:kinetic-desktop-full
FROM osrf/ros:melodic-desktop-full

RUN apt-get update && apt-get install -y --no-install-recommends vim && rm -rf /var/lib/apt/lists/*

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
  ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
  ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics
