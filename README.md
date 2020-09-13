# HelmetDetection
# The Problem Statement

The main problem statement being dealt with in this project is the detection of non-legal motorcyclists on Indian roads. This is being implemented as an  object detection and 
recognition algorithm from frames that have been captured off a video that is taken in traffic. This video could either be taken from a POV camera (for example in a police car) or from a roadside mounted camera and should work for both cases.

# Stages of the project

- Labelling and Data Preperation
- Object Detection
- Image Classification

## Stage 1 : Labelling and data preperation : Techniques used to generate Data and sources of initial images
To start off with, as far as I am aware, there was no good annotated dataset for this problem statement. An initial dataset with dashcam images from Hyderabad and Bangalore was found and used from [here](https://www.kaggle.com/manjotpahwa/indian-driving-dataset).


Next, to deal with the annotations, the images had to be labelled with bounding boxes around legal and non-legal riders. [This](https://www.makesense.ai/) website was used for an initial set of annotations. Along with this, images where there were no overlapping bike riders could have their bounding boxes drawn around them using Image segmentation. The bounding boxes would then just have to be annotated to the right class. This is one of the techniques that are used to speed up the annotation process pretty drastically, especially considering how long it takes to manually draw bounding boxes.


Another technique that was used to increase the speed of annotations was active learning, where the model was trained on the initial set of annotated images and the predictions from this model were then checked, corrected and then added to the set of annotated images as well. This increased the speed of the annotations even more. 

## Stage 2 : Object Detection : Detection of bikes with riders of all orientations and distances from camera
The object detection phase of this project deals with detecting all bike riders in the images. Initially, this phase was tried with the detection of both legal and illegal riders seperately but as the images from th two classes are extremely similar, this proved to be ineffective. 

The object detection was done using transfer learning on the pre-trained YOLO v-5 model.The results after the detector was trained are shown in the results section.

## Stage 3 : Image Classification : Classification of the detected bikes into legal and non-legal
The annotated boundong boxes were cropped to make up the training set for the classifier (A drastic improvement can be made to performance by altering this step slightly and using the results from the object detection as the training samples rather than the hand annotated images as the sizes of the boxes don't really match up perfectly). A range of networks were tested, ranging from EfficientNets to shallow convolutional neural networks. In the end, a form of shallow convolutional neural network was able to give out the best results which are diplayed in the section below. 

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
The final (and best) epoch of the training of the YOLOv5 model has been shown below : 
![alt text](https://github.com/SanjitKad/HelmetDetection/blob/master/Images/Training%20results/Train_epoch.jpg)

From here it can be seen that the mAP is around 83% and the recall is about 85%. This is inclusive of a GIOU estimate and can be increased further by having more training datapoints of real images to optimize the bounding box predictions. A larger amount of training data would really help the model in dealing with edge cases for example, parked motorcycles by the side of the road with people still on them and so on.

### Confusion Matrix of classification :
The confusion matrix of the general image classification (Cropped detected images of all sizes in the "Test" folder) produced the following confusion matrix on a test set. This gives us a precision, recall and F1 score of about 75%. (The results can be seen in the Full_Classifier.ipynb notebook) The main goal here would be to reduce the True Legal -Predicted Non legal amount and increase the Treu Nonlegal-Predicted Non legal amount as those would be the important ones under consideration for further action (the predicted legal set is not going to be considered anyways). 


|                         | True Non Legal            | True Legal      |
| ----------------------  |:-------------------------:| ---------------:|
| *Predicted Non-Legal*   | 07                        | 02              |
| *Predicted Legal*       | 10                        | 22              |


However, these images consist of bikers/riders that are really far away from the camera as well. They are in fact so far away that it would be difficult even for a human to make an accurate prediction manually. Hence, the test set was trimmed down to contain images where the bikers and the license plates would be clearly visible (in this case, dimensions larger than 300 pixels). In this case, the classification algorithm producded a much better output with a precision and recall of over 95% on multiple tests. This could be improved even further by training on more real world data specific to the region under consideration. 




## Future Work :

1. Capturing and framing of videos from the cities in question so as to best suit the rules and regulations of the region. For example, the images used here are from Hyderabad when the rule regarding helmets for pillions was not enforced strictly. This would be different in the case of Bangalore and would need data that is local to each city/region.

2. To work on more unsupervised/semi-supervised techniques to annotate data as this would be the slowest and more laborious part of the pipeline that could definitely be made faster and of better quality. 

3. To use the actual outputs from the object recognition algorithm to train the classification algorithm as they would best represent the bounding boxes that would be the input for the classification algorithm during testing as well. 

