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

## Stage 3 : Image Classification : Classification of the detected bikes into legal and non-legal

## Results : 

## Future Work :

