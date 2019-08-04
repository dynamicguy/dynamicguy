---
title: Fix for python Library mismatch during opencv build
date: 2019-08-04T18:01:50.390Z
description: Fix for python Library mismatch during opencv build
image: /img/opencv_logo_with_text_svg_version.svg
---
```
cmake -G “Unix Makefiles” -D CMAKE_CXX_COMPILER=/usr/bin/g++ CMAKE_C_COMPILER=/usr/bin/gcc -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=OFF -D WITH_OPENGL=ON -D BUILD_FAT_JAVA_LIB=ON -D INSTALL_TO_MANGLED_PATHS=ON -D INSTALL_CREATE_DISTRIB=ON -D INSTALL_TESTS=ON -D ENABLE_FAST_MATH=ON -D WITH_IMAGEIO=ON -D BUILD_SHARED_LIBS=OFF -D WITH_GSTREAMER=ON -D PYTHON_LIBRARY=$(python-config –prefix)/lib/libpython2.7.dylib -D PYTHON_INCLUDE_DIR=$(python-config –prefix)/include/python2.7 -D PYTHON_PACKAGES_PATH=$(python-config –prefix)/lib/python2.7/site-packages ..make -j4sudo make install
```
