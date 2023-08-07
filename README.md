Building a Face Detector & Age Group Predictor App
==========

This application, designed as a protoype, detects a person's face within 
an image and predicts their age group. A practical use of this app would 
be in a retail environment, where cameras can predict customers' ages and 
derive analytic data for target consumers. 

For testing the application, the publicly available IMDB-WIKI dataset was used.
The HAAR Cascade algorithm is used to detect faces, and a logistic regression
classifier is used as the age-predictive model. Additionally, a CNN model has
been trained to compare its accuracy results with the logistic regression 
classifier's.

## Tools

This app is programmed fully in Python and written in Google Colab. The
following tools are utilized:
  * Tensorflow (CNN model)
  * OpenCV (HAAR Cascade)
  * scikit-learn (logistic regression classifier)

These tools perform well for testing-purposes, thus it is especially
beneficial in the works of a prototype. These tools are of great caliber and
yield desired results without excessive consumption of resources.

## Challenges

The WIKI dataset contains 62,328 images, but not all of them are ideal for 
model training. For instance, only a handful of images refuse to convert to
grayscale for the HAAR Cascade algorithm to run. The real age labeled with 
each image is sometimes negative, and quite often images appear that do not
even contain a person. A couple of filter mechanisms used to acquire "clean" 
data is by error handling, and checking if a face is detected at all before
any proceessing. These guidelines will ensure that most of the data feeding 
into the model is useful. 

Another useful method to filter out images for age prediction is utilizing the
IoU score (Intersection over Union). Each image comes with the coordinates of 
where the face is located, but sometimes these coordinates are wrong. A way to
bypass this is by checkinf if the HAAR Cascade algorithm intersects with the
real coordinates more than 50%; if so, that data proves more useful for the 
age-prediction portion of the app.
9










