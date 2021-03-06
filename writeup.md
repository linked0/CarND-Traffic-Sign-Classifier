# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./images/data_anal_vis.png "Data Analyze"
[image2]: ./images/traffic_sign_gray.png "Gray"
[image4]: ./new_signs3/Ahead_only.jpg "Ahead only"
[image5]: ./new_signs3/Children_crossing.jpeg "Children crossing"
[image6]: ./new_signs3/Priority_road.jpg "Priority road"
[image7]: ./new_signs3/Right-of-way_at_the_next_intersection.jpeg "Right of way at the next intersection.jpeg"
[image8]: ./new_signs3/Speed_limit_60km.jpeg "Speed limit 60 km/h"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/linked0/CarND-Traffic-Sign-Classifier/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is (34799, 32, 32, 3)
* The size of the validation set is (4410, 32, 32, 3)
* The size of test set is (12630, 32, 32, 3)
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because color values don't affect the performace.

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image2]

As a last step, I normalized the image data because I'd like in this process for each feature to have a similar range so that our gradients don't go out of control 


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 1st (3x3) | 1x1 stride, valid padding, outputs 30x30x8 	|
| RELU					|												|
| Convolution 2nd (3x3) | 1x1 stride, valid padding, outputs 28x28x16	|
| Max pooling		| 2x2 stride,  outputs 14x14x16 			|
| RELU					|												|
| Dropout     	        | keep probability 0.7 for training 	|
| Convolution 3rd (3x3) | 1x1 stride, valid padding, outputs 12x12x32 |
| RELU					|												|
| Convolution 4th (3x3) | 1x1 stride, valid padding, outputs 10x10x32 |
| RELU					|												|
| Max pooling		| 2x2 stride,  outputs 5x5x32 			|
| Convolution 5th (3x3) | 1x1 stride, valid padding, outputs 3x3x32 |
| RELU					|												|
| Fully connected 1st	| input = 288, output = 120 |
| RELU					|												|
| Dropout     	        | keep probability 0.7 for training 	|
| Fully connected 2nd | input = 120, output = 84 |
| RELU					|												|
| Dropout     	        | keep probability 0.7 for training 	|
| Fully connected 3rd | input = 84, output = 43 |
| Softmax				|        									|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

Optimizer: AdamOptimizer
Learning rate: 0.001
Dropout probability: 0.7
Batch size: 128
Epoch: 15

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 100%
* validation set accuracy of 97.2% 
* test set accuracy of 95.3%

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?<br>
<i>First, I chose the original LeNet model. I just wanted to start with the LeNet model and improve the model step by step. The original LeNet model was not so deep and had not the dropout step.</i>

* What were some problems with the initial architecture?<br>
<i>The test set accuracy was below 90% which was not met with the project requirement and the model has an underfitting problem.</i>

* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.<br>
<i>I added three more Convolutional layers and some dropout steps.</i>

* Which parameters were tuned? How were they adjusted and why?<br>
<i>I found that the learning rate really affect the model performace. In this project, It was the most important parameter.</i>

* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?<br>
<i>I think a deeper Convolutional network model with dropout layer is better.</i>

If a well known architecture was chosen:
* What architecture was chosen?<br>
<i>LeNet</i>

* Why did you believe it would be relevant to the traffic sign application?<br>
<i>It's a start point for image classification problems.</i>

* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?<br>
<i>With the deeper network model and dropout layers, I got a good result.</i>
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:
<hr>

![alt text][image4] Ahead only
<hr>

![alt text][image5] Children crossing
<hr>

 ![alt text][image6] Priority road
 <hr>

![alt text][image7] Right-of-way at the next intersection
<hr>

![alt text][image8] Speed limit (60km/h)

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	| 
|:---------------------:|:-------------------:| 
| Ahead only    | Ahead only  				| 
| Right-of-way at the next intersection | Right-of-way at the next intersection |
| Priority road	| Priority road		|
| Children crossing | Priority road		|
| Speed limit (60km/h)		| Speed limit (60km/h)   |


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of 95.3%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 16th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a "Ahead only" sign (probability of 99.9), and the image does contain a stop sign. The top five soft max probabilities were

| Probability           |     Prediction        | 
|:---------------------:|:---------------------:| 
| 9.999942e-01          | Ahead only            | 
| 4.385554e-06          | Yield                 |
| 8.149665e-07          | Children crossing     |
| 2.934660e-07          | Speed limit (60km/h)  |
| 2.244020e-07          | Turn left ahead       |


For the fourth image, the model is relatively sure that this is a "Priority road" sign (probability of 59.6), and the image does contain a "Children crossing" sign. The top five soft max probabilities were

| Probability           |     Prediction        | 
|:---------------------:|:---------------------:| 
|      0.595587     | Priority road            | 
| 0.243497          | Right-of-way at the next intersection |
| 0.037928          | End of no passing     |
| 0.033671          | Ahead only  |
| 0.029374          | Slippery road       |
 

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?
