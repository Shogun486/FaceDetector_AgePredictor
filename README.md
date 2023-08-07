Building a Face Detector & Age Group Predictor App
==========

This application, designed as a protoype, detects a person's face within 
an image and predicts their age group. A practical use of this app would 
be in a retail environment, where cameras can predict customers' ages and 
derive analytic data for target consumers. 

For testing the application, the publicly available IMDB-WIKI dataset was 
used. All installation procedures to acquire this data is explicitly labeled 
in the Colab notebooks. 

The HAAR Cascade algorithm is used to detect faces, and a logistic regression
classifier is used as the age-predictive model. SIFT is used to extract key 
features from each image for training. Additionally, a CNN model has
been trained to compare its accuracy results with the logistic regression 
classifier's. 

## Tools

This app is programmed fully in Python and written in Google Colab. The
following tools are utilized:
  * Tensorflow (CNN model)
  * OpenCV (HAAR Cascade and SIFT)
  * scikit-learn (logistic regression classifier)

These tools perform well for testing-purposes, thus it is especially
beneficial in the works of a prototype. These tools are reliable 
and yield desired results without excessive consumption of resources.

## Challenges

The WIKI dataset contains 62,328 images, but not all of them are ideal for 
model training. For instance, only a handful of images do not convert to
grayscale (which is required for the HAAR Cascade algorithm to run). The 
real age labeled with each image is sometimes negative, and quite often 
images appear that do not even contain a person. A couple of filter 
mechanisms used to acquire "clean" data is by error handling, and checking 
if a face is detected at all before any proceessing. These guidelines will 
ensure that most of the data feeding into the model is useful. 

Another useful method to filter out images for age prediction is utilizing the
IoU score (Intersection over Union). Each image comes with the coordinates of 
where the face is located, but sometimes these coordinates are wrong. A way to
bypass this is by checkinf if the HAAR Cascade algorithm intersects with the
real coordinates more than 50%; if so, that data proves more useful for the 
age-prediction portion of the app.

## IoU Crop - Filtering the dataset

Filtering out data is the first step before processing any of it. The 
IoU_Crop.ipynb is a multi-threaded program used to iterate over the entire 
WIKI dataset, parsing out corrupt images while also collecting the IoU score 
for each one. The average IoU score comes out to be approximately 70%, but 
modifying the attributes of the HAAR Cascade algorithm may yield higher 
results. Since the WIKI dataset is so diverse, there isn't a hard and fast way 
to optimize its usage. Rather, experimentation with these attributes is the 
key to attain great results. 


## Age Prediction

Now that the dataset has been filtered, the next step is to predict age groups.
Almost all image processing, especially when dealing with machine learning, 
makes use of classifying/labeling the dataset. Once the dataset has been labeled,
it can be trained to predict. The training model used in AgePrediction.ipynb is a
logistic regression classifier, which is a supervised meachine learning approach.
What this means is that the data can clearly be categorized. In this case, the
data can be separated into 5 age groups: [0 - 20), [20 - 40), [40 - 60), [60 - 80), 
and [80 - 100].

The IoU-cropped images can indeed be used to train the logistic regression classifier, 
but it is generally advised to isolate experiments. Therefore, it's best to use 
the WIKI pre-cropped faces dataset available here. Once the age-prediction model 
is optimized, it's as simple as feeding the IoU-cropped images into the training 
and testing set.




















