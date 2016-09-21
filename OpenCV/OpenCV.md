# OpenCV Installation

Follow the link: http://www.samontab.com/web/2012/06/installing-opencv-2-4-1-ubuntu-12-04-lts/

This applies to OpenCV 2.4.X versions. Look for the zip files online for 2.4.1-2.4.9 versions.

##For Local Installation within specified home directory
Add this to you CMake compile options

 cmake -DCMAKE_INSTALL_PREFIX=/home/jay/opencv-2.4.x/release/installed -DCMAKE_BUILD_TYPE="Release" .. 

Refer to this link for utilizing two versions of OpenCV side by side: http://code.litomisky.com/2014/03/09/how-to-have-multiple-versions-of-the-same-library-side-by-side/


## ROS and OpenCV

ROS installs OpenCV libs in your filesystem, because many of the vision pipeline libraries eg. image_transport, cv_bridge has opencv dependencies. 
To explicitly compiles ROS packages using your standalone OpenCV you can set in your .bashrc

* export CMAKE_PREFIX_PATH=/home/jay/opencv-2.4.9/Release:$CMAKE_PREFIX_PATH

This will ensure that the Standalone OpenCV is picked first for compilation. As default ROS uses its own  OpenCV libs.
To check again, try the command 

* echo $CMAKE_PREFIX_PATH

Most of the functionality of OpenCV can be used except for the nonfree libraries which has SIFT/SURF. 

To use SIFT/SURF, The SIFT class can be initialized by calling  initModule_nonfree(); at the beginning

## Pro Tips

* To check version: pkg-config --modversion opencv : 

* catkin_make VERBOSE=1 can help in checking how libraries are linked at compilation.











