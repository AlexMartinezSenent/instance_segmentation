# instance_segmentation
C++ implementation of an instance segmentation deep learning model to mask the object's pixels from the input images. The model used was Mask RCNN (Inception v2 2018 trained on COCO classes). The model, already trained and exported is loaded into the pipeline using the OpenCV DNN module (that accepts models in different formats) and then the output is postprocessed to draw bounding boxes around each class instance and color a mas on top of the segmentation output. Additionally, a close-up and a segmented image is saves for each instance.
![test](https://user-images.githubusercontent.com/44910949/152676382-65474cc1-2bfd-4f18-afcb-e9dc87355d8d.jpg)
![test_mask_rcnn_out](https://user-images.githubusercontent.com/44910949/152676386-a075392b-341c-4d72-9f4e-2b4848b147ea.jpg)

## Dependencies

-  C++ compiler for c++11 or later. \
-  OpenCV and opencv_conrib modules for c++ (OpenCV 4 version 4.5.5 was used, 4.0.0 or later required)

## Intsallation

Download and install OpenCV library, if the OS is Unix based, then make sure, when configuring the cmake recipe, to state the path to opencv contrib modules source directory. It can be done with the cmake gui tool or with terminal comands as follows: (this is an example with my local path, follow the official installation guide for full instructions)\
```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_C_EXAMPLES=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/Alex/codes/aux_libs/opencv_contrib/modules \
    -D BUILD_EXAMPLES=ON ..
```

## Compilation

It may be necessary to include a flag to each of the opencv_contrib modules as compiler argument to successfully compile segmentation.cpp. \
The used command for compiling the code is:
```
    g++ -I/usr/local/include/opencv4/ -L/usr/local/lib/ segmentation.cpp  -lopencv_dnn -lopencv_imgproc -lopencv_core -lopencv_highgui -lopencv_imgcodecs -lopencv_videoio -o segmentation.out
```
But depending on the installation of the opencv library the paths may be different.

## Execution 

The application can accept both images and video inputs. Select the input file as ```--image=/path/to/image.extension``` or ```--video=/path/to/video.extension``` after the name of the compiled object.

On Ubuntu terminal, execute the output of the compilation as:
```
./segmentation.out --image=test.jpg
```
This will produce a file called ```test_mask_rcnn_out.jpg``` with all bounding boxes and masks overlays on the input image, and two files for each instance following the naming structure:
-  ```test_mask_rcnn_out_className_detectionId.jpg``` for the bounding box image.
-  ```test_mask_rcnn_out_className_detectionId_seg.jpg``` for the segmented image.

## Known Issues

When the input is a video stream, depending on the size of the bounding box, its location an the region of the frame where the object is located, the ROI bounds may be out of range of the matrix, resulting in the abortion of the application. It is recommended to use image input files.

## Credits

The inspiration and part of the code for the implementation of the application is based on the tutorial from LearnOpenCV found in https://learnopencv.com/deep-learning-based-object-detection-and-instance-segmentation-using-mask-rcnn-in-opencv-python-c/
\
The code can be found in the repository at https://github.com/spmallick/learnopencv/tree/master/Mask-RCNN
\
The model used can be downloaded from tensorflow.com using:
``` 
wget http://download.tensorflow.org/models/object_detection/mask_rcnn_inception_v2_coco_2018_01_28.tar.gz 
tar zxvf mask_rcnn_inception_v2_coco_2018_01_28.tar.gz
```
The test image has been taken for the purpose of testing the capabilities of the model to detect the available calsses whereas the desk and desk2 images are samples from the internet.
