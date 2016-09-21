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


### ROS + OpenCV + Nonfree

Most of the functionality of OpenCV can be used except for the nonfree libraries which has SIFT/SURF. 

To use SIFT/SURF, The SIFT class can be initialized by calling  initModule_nonfree(); at the beginning. Not doing this can cause an error like this:
This is how SIFT class is called for OpenCV 2.4. I currently use ROS Indigo+14.04. Hence I have OpenCV 2.4 installed by ROS.

'''
 undefined reference to `VTT for cv::SIFT
 undefined reference to `cv::SIFT::SIFT(int, int, double, double, double)'

'''

Make sure you have nonfree installed as this does not ship in together.

'''
sudo add-apt-repository --yes ppa:xqms/opencv-nonfree
sudo apt-get update 
sudo apt-get install libopencv-nonfree-dev
'''


## Pro Tips

* To check version: pkg-config --modversion opencv : 

* catkin_make VERBOSE=1 can help in checking how libraries are linked at compilation.

* SET("OpenCV_DIR" "PATH/TO/CMake/build") can also be used to set path to standalone installations. 

* OpenCV 3.x.x has moved nonfree features to opencv_contrib repo. Make sure to set the headers accordingly.    #include "opencv2/xfeatures2d.hpp" 	
  Make sure to refer to this link: https://github.com/itseez/opencv_contrib/


## Useful Links

I ll keep adding more as I can. In case I missed something, you can always:

* http://stackoverflow.com/questions/9742052/cmake-is-not-working-in-opencv-c-project

* http://stackoverflow.com/questions/27533203/how-do-i-use-sift-in-opencv-3-0-with-c	

* http://code.litomisky.com/2014/03/09/how-to-have-multiple-versions-of-the-same-library-side-by-side/

* http://answers.opencv.org/question/12074/cmake-opencv_dir/

* http://www.samontab.com/web/2012/06/installing-opencv-2-4-1-ubuntu-12-04-lts/

* http://answers.ros.org/question/209358/cant-find-nonfree-module-opencv/











