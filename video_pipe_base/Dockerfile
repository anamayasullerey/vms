# Use the official Python image as the base image
FROM python:latest

# Set the working directory
RUN mkdir /proj
WORKDIR /proj

# Install necessary system packages
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    git \
    wget \
    unzip

RUN apt-get install -y vim
RUN apt-get install -y ffmpeg

# OpenCV related install
# ======================
ARG OPENCV_VERSION='4.x'
# Install the dependencies
# GUI 
RUN apt-get install -y libgtkglext1-dev libgtk2.0-dev libvtk6-dev

# Media I/O:
RUN apt-get install -y zlib1g-dev libjpeg-dev libwebp-dev libpng-dev libtiff5-dev \
                       libopenexr-dev libgdal-dev

# Video I/O:
RUN apt-get install -y libdc1394-22-dev libavcodec-dev libavformat-dev libswscale-dev \
                       libtheora-dev libvorbis-dev libxvidcore-dev libx264-dev yasm \
                       libopencore-amrnb-dev libopencore-amrwb-dev libv4l-dev libxine2-dev

# Parallelism and linear algebra libraries:
RUN apt-get install -y libtbb-dev libeigen3-dev

# Python:
RUN apt-get install -y python-dev  python-tk  pylint  \
                       python3-dev python3-tk pylint3 python3-numpy flake8

# Java:
RUN apt-get install -y ant default-jdk

# Documentation and other:
RUN apt-get install -y doxygen

# Install the library

RUN wget https://github.com/opencv/opencv/archive/4.x.zip
RUN unzip 4.x.zip && rm 4.x.zip
RUN mv opencv-4.x opencv
RUN cd opencv && \
    mkdir build && \
    cd build && \
    cmake -DWITH_OPENGL=ON -DFORCE_VTK=ON -DWITH_TBB=ON -DWITH_GDAL=ON -DWITH_XINE=ON -DENABLE_PRECOMPILED_HEADERS=OFF .. && \
    make -j8 && \
    make install && \
    ldconfig

RUN pip install --upgrade pip
RUN pip install opencv-python

# if [ $OPENCV_CONTRIB = 'YES' ]; then
#   wget https://github.com/opencv/opencv_contrib/archive/${OPENCV_VERSION}.zip
#   unzip ${OPENCV_VERSION}.zip && rm ${OPENCV_VERSION}.zip
#   mv opencv_contrib-${OPENCV_VERSION} opencv_contrib
#   mv opencv_contrib OpenCV
# fi
# cmake -DWITH_OPENGL=ON -DFORCE_VTK=ON -DWITH_TBB=ON -DWITH_GDAL=ON \
#       -DWITH_XINE=ON -DENABLE_PRECOMPILED_HEADERS=OFF \
#       -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules ..
# 
# Copy the requirements.txt file into the container
# COPY requirements.txt .
# 
# Install any additional packages specified in requirements.txt
# RUN pip install --no-cache-dir -r requirements.txt
# 
COPY support_files/bashrc /root/.bashrc
COPY support_files/aliases /root/.aliases
# 
RUN mkdir test_video
RUN mkdir test_video/cpp
COPY support_files/DisplayVideo.cpp test_video/cpp
COPY support_files/CMakeLists.txt test_video/cpp
RUN mkdir test_video/python
COPY support_files/display_video.py test_video/python
 
ENV PYTHONPATH "/proj"
