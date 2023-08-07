Building a Face Detector & Age Group Predictor App
==========

This application, designed as a protoype, detects a person's face within 
an image and predicts their age group. A practical use of this app would 
be in a retail environment, where cameras can predict customers' ages and 
derive analytic data for target consumers. 

For testing the application, the publicly available IMDB-WIKI dataset was used.

This app is programmed completely in Python and written in Google Colab. The
following tools are utilized:
  * Tensorflow (CNN model)
  * OpenCV (HAAR Cascade)
  * scikit-learn (logistic regression classifier)

The HAAR Cascade algorithm is used to detect faces, and a logistic regression
classifier is used as the age-predictive model. Additionally, a CNN model has
also been trained to compare its accuracy results with the logistic regression 
classifier's.





