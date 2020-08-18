# HelmetDetection

# Stages of the project

- Labelling and Data Preperation
- Object Detection
- Image Classification

## Stage 1 : Labelling and data preperation : Techniques used to generate Data and sources of initial images
To start off with, as far as I am aware, there was no good annotated dataset for this problem statement. An initial dataset with dashcam images from Hyderabad and Bangalore was found and used from [here](https://www.kaggle.com/manjotpahwa/indian-driving-dataset).


Next to deal with the annotations, the images had to be labelled with bounding boxes around legal and non-legal riders. [This](https://www.makesense.ai/) website was used for an initial set of annotations. Along with this, images where there were no overlapping bike riders could have their bounding boxes drawn around them using Image segmentation. The bounding boxes would then just have to be annotated to the right class. This is one of the techniques that are used to speed up the annotation process pretty drastically, esoecially considering how long it takes to manually draw bounding boxes.


Another technique that was used to increase the speed of annotations was active learning, where the model was trained on the initial set of annotated images and the predictions from this model were then checked, corrected and then added to the set of annotated images as well. This increased the speed of the annotations even more. 

## Stage 2 : Object Detection : Detection of bikes with riders of all orientations and distances from camera
The object detection phase of this project deals with detecting all bike riders in the images. Initially, this phase was tried with the detection of both legal and illegal riders but as the images from th two classes are extremely similar, this prved to be ineffective. 

The object detection was done using the pre-trained YOLO v-5 model.The results after the detector was trained are shown in the results section.

## Stage 3 : Image Classification : Classification of the detected bikes into legal and non-legal
The annotated boundong boxes were cropped and the detectors predictions were labelled and cropped too, to make up the training set for the classifier. A range of networks were tested, ranging from EfficientNets to shallow convolutional neural networks. In the end, a form of convolutional neural network was able to give out the best results which are diplayed in the section below. 

If the system needs to be applied in the real world, then assuming that the number plates of all the non-legal riders would have to be read, only the detected rider images that are fairly large would have to be classified. This would make it much easier for the classifier to differentiate between the two classes. 

## Results : 

### Examples of some of the raw images from the dataset :
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Input_Images/0000016_leftImg8bit.jpg)
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Input_Images/0000213_leftImg8bit.jpg)

### Examples of some of the labelled images (after Stage 1):
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Annotated_Images/i1.jpg)
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Annotated_Images/i2.jpg)

### Examples of some of the cropped riders (after Stage 2):
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Cropped_riders/0004979_leftImg8bit32.jpg) ![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Cropped_riders/0004980_leftImg8bit39.jpg)![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Cropped_riders/0005016_leftImg8bit49.jpg) ![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Cropped_riders/0005037_leftImg8bit53.jpg) ![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Cropped_riders/0005915_leftImg8bit182.jpg)

### Object Detection results :
The final epoch oh training of the YOLOv5 model has been shown below : 




## Future Work :

