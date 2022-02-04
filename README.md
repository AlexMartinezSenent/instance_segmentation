# instance_segmentation
C++ implementation of an instance segmentation deep learning model to mask the object's pixels from the input images.


cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_C_EXAMPLES=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/Alex/codes/aux_libs/opencv_contrib/modules \
    -D BUILD_EXAMPLES=ON ..



    g++ -I/usr/local/include/opencv4/ -L/usr/local/lib/ proofofconcept.cpp  -lopencv_dnn -lopencv_imgproc -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_videoio -o proof