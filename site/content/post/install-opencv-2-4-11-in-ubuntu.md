---
title: Install OpenCV-2.4.11 in ubuntu
date: 2019-08-04T18:38:25.180Z
description: Install OpenCV-2.4.11 in ubuntu
image: /img/opencv_logo_with_text_svg_version.svg
---
TLDR: curl -L https://gist.github.com/dynamicguy/3d1fce8dae65e765f7c4/raw/21e9f30cd14ac6fd8b9f82eb7fc52137e1492bae/install-opencv-2.4.11-in-ubuntu.sh | sh

install the prerequisite dependencies

sudo apt-get update

sudo apt-get install -y build-essential

sudo apt-get install -y cmake

sudo apt-get install -y libgtk2.0-dev

sudo apt-get install -y pkg-config

sudo apt-get install -y python-numpy python-dev

sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install -y libjpeg-dev libpng-dev libtiff-dev libjasper-dev

even more deps

sudo apt-get -qq install libopencv-dev build-essential checkinstall cmake pkg-config yasm libjpeg-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev python-dev python-numpy libtbb-dev libqt4-dev libgtk2.0-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils

download opencv-2.4.11

wget http://downloads.sourceforge.net/project/opencvlibrary/opencv-unix/2.4.11/opencv-2.4.11.zip

unzip opencv-2.4.11.zip

cd opencv-2.4.11

mkdir release

cd release

compile and install

cmake -G “Unix Makefiles” -D CMAKE_CXX_COMPILER=/usr/bin/g++ CMAKE_C_COMPILER=/usr/bin/gcc -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D BUILD_FAT_JAVA_LIB=ON -D INSTALL_TO_MANGLED_PATHS=ON -D INSTALL_CREATE_DISTRIB=ON -D INSTALL_TESTS=ON -D ENABLE_FAST_MATH=ON -D WITH_IMAGEIO=ON -D BUILD_SHARED_LIBS=OFF ..

make all -j4 #4 cores

sudo make install

ignore libdc1394 error http://stackoverflow.com/questions/12689304/ctypes-error-libdc1394-error-failed-to-initialize-libdc1394

python

\* import cv2

\* cv2.SIFT

<built-in function SIFT*

OR

you can just download this shell script https://gist.github.com/dynamicguy/3d1fce8dae65e765f7c4 and execute it with sudo use
