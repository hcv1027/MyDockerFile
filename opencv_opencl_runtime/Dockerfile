# FROM nvidia/opencl:devel-ubuntu16.04
FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04

# OpenCL runtime
RUN apt-get update && apt-get install -y --no-install-recommends \
    ocl-icd-libopencl1 \
    clinfo && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/OpenCL/vendors && \
    echo "libnvidia-opencl.so.1" > /etc/OpenCL/vendors/nvidia.icd

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility

# OpenCL devel
RUN apt-get update && apt-get install -y --no-install-recommends \
    ocl-icd-opencl-dev && \
    rm -rf /var/lib/apt/lists/*

# OpenCV required build dependencies
# https://docs.opencv.org/3.4.10/d2/de6/tutorial_py_setup_in_ubuntu.html
RUN apt-get update && apt-get install -y --no-install-recommends \
    git vim cmake gcc g++ wget \
    python3-dev python3-numpy \
    libavcodec-dev libavformat-dev libswscale-dev \
    libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev \
    libgtk2.0-dev libgtk-3-dev \
    libpng-dev libjpeg-dev libopenexr-dev libtiff-dev libwebp-dev \
    libjasper-dev \
    build-essential && \
    rm -rf /var/lib/apt/lists/*
