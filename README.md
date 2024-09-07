Building a Face Detector & Age Group Predictor App
==========

This application, designed as a protoype, detects a person's face within 
an image and predicts their age group. A practical use of this app would 
be in a retail environment, where cameras can predict customers' ages and 
derive analytic data for target consumers. 

For testing the application, the publicly available [IMDB-WIKI] dataset was 
used. All installation procedures to acquire this data is explicitly labeled 
in the Google Colab notebooks, along with all relevant implementations. 

The HAAR Cascade algorithm is used to detect faces, and a logistic regression
classifier is used as the age-predictive model. SIFT is used to extract key 
features from each image for model training. Additionally, a CNN model has
been trained to compare its accuracy results with the logistic regression 
classifier's. 

## Tools

This app is programmed entirely in Python and runs in Google Colab. The
following tools are utilized:
  * Tensorflow (CNN model)
  * OpenCV (HAAR Cascade and SIFT)
  * scikit-learn (logistic regression classifier)

These tools perform well for testing-purposes, thus it is especially
beneficial in the works of a prototype. These tools are reliable 
and yield desired results without excessive consumption of resources.

## Challenges

The [WIKI dataset] contains 62,328 images, but not all of them are ideal for 
model training. For instance, only a handful of images do not convert to
grayscale (which is required for the HAAR Cascade algorithm to run). The 
real age labeled with each image is sometimes negative, and quite often 
images appear that do not even contain a person. A couple of filter 
mechanisms used to acquire "clean" data is by error handling and checking 
if a face is detected at all before any processing. These guidelines will 
ensure that most of the data feeding into the model is useful. 

Another efficient method to filter out images for age prediction is utilizing the
IoU score (Intersection over Union). Each image comes with the coordinates of 
where the face is located, but sometimes these coordinates are wrong. A way to
bypass this is by checking if the HAAR Cascade algorithm intersects with the
real coordinates' area more than 50%; if so, that data proves more useful for the 
age-prediction portion of the app.

## IoU Crop - Filtering the dataset (see [IoU_Crop.ipynb])

Filtering out data is the first step before processing any of it. The 
[IoU_Crop.ipynb] is a multi-threaded program used to iterate over the entire 
WIKI dataset, parsing out corrupt images while also collecting the IoU score 
for each one. The average IoU score comes out to be approximately 70%, but 
modifying the attributes of the HAAR Cascade algorithm may yield higher 
results. Since the WIKI dataset is so diverse, there isn't a hard and fast way 
to optimize its usage. Rather, experimentation with these attributes is the 
key to attaining great results. 


## Age Prediction (see [AgePrediction.ipynb])

### How Classifiers Work
Now that the dataset has been filtered, the next step is to predict age groups.
Almost all image processing, especially when dealing with machine learning, 
makes use of classifying/labeling the dataset. Once the dataset has been labeled,
it can be trained to predict. The training model used in [AgePrediction.ipynb] is a
logistic regression classifier, which is a supervised machine learning approach.
What this means is that the data can clearly be categorized. In our case, the
data can be separated into 5 age groups: [0 - 20), [20 - 40), [40 - 60), [60 - 80), 
and [80 - 100].

### SIFT
Next, there has to be a way for the model to recognize images and categorize
them. This is where feature-extraction methods like SIFT come in. SIFT basically 
gathers key features from each image. The model will start recognizing patterns. 
Different people with the same age group tend to have similar features, so SIFT
is a good place to start. SIFT maps keypoints on every image, along with descriptors
which spatially describe each keypoint. Many image processing systems utilize a
2048-dimensional linear feature vector, so that's a good place to start. Each 
descriptor in SIFT is a 128-bit vector, so 16 of them will equal 2048. SIFT may not 
be able to detect enough keypoints on each image such that the 2048 amount is reached, 
thus there needs to be some manual padding (which can be seen in the code).

### Best Practice
The IoU-cropped images can indeed be used to train the logistic regression classifier, 
but it is generally advised to isolate experiments. Therefore, it's best to use 
the WIKI pre-cropped faces dataset available [here]. Once the age-prediction model 
is optimized, it's as simple as feeding the IoU-cropped images into the training set.

## Improving The Model & Comparing Results

### Comparing to a Pre-Trained Model (see [Wiki_PreTrainedModel.ipynb])
The creators of the dataset also have a pretrained model. Upon comparing their model with
mine on a particular set of images, both reached an accuracy rate of approximately 70%. 
However, this doesn't mean both models are equally accurate. Their's is a CNN model, whereas
mine's is a logistic regression classifier. CNN models are known for better image processing, 
and indeed their accuracy rate is better on other sets of images. However, this means we
are on the right track to predicting the correct age group. 

### Creating a CNN Model (see [CNN_Model.ipynb])
Since the creators of the dataset had a CNN model, I thought I should create my own and compare
results. Again, I trained the images on the pre-cropped dataset they have to see the results
purely. There are many factors that go into training a CNN model to reach its peak accuracy.
Different image sizes, kernel sizes, etc. play a role into how the model is trained. My CNN model
was able to reach a 60% accuracy rate on a particular set of images. The accuracy rate isn't high 
because many of the pre-cropped images also need just as much filtering as we've done before. But
upon just supplying the IoU-cropped images, the accuracy rate went up to 70%. This just shows that 
even the smallest amount of tinkering can make a big difference in your model. Models need to
see "clean" data in order to fully understand it: a simple IoU crop was able to boost this score
considerably. 

## Conclusion
All of the parts needed to detect a person's face and predict their age group are in place. We were able to 
parse through a public dataset containing several thousands of images, filtering them and only keeping
images that are useful. A little thinking outside the box allowed us to improve the face capture by
using the IoU concept. Increasing the accuracy rate of a model is highly dependent on the data it reads
and the attributes used to process that data. In this project, we were able to learn about key machine
learning concepts and how to build a practical application that can be used as a prototype for retail
environments and those that serve similar purposes.


[IoU_Crop.ipynb]: https://github.com/Shogun486/FaceDetector_AgePredictor/blob/main/IoU_Crop.ipynb
[AgePrediction.ipynb]: https://github.com/Shogun486/FaceDetector_AgePredictor/blob/main/AgePrediction.ipynb
[Wiki_PreTrainedModel.ipynb]: https://github.com/Shogun486/FaceDetector_AgePredictor/blob/main/Wiki_PreTrainedModel.ipynb
[CNN_Model.ipynb]: https://github.com/Shogun486/FaceDetector_AgePredictor/blob/main/CNN_Model.ipynb
[IMDB-WIKI]: https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/
[here]: https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/static/wiki_crop.tar
[WIKI dataset]: https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/static/wiki.tar.gz


















