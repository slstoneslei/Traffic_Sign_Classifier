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

[image1]: ./examples/visualization.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[image7]: ./examples/placeholder.png "Traffic Sign 4"
[image8]: ./examples/placeholder.png "Traffic Sign 5"

[image10]: ./examples/TrafSign_labels.png "TrafSign_labels"
[image11]: ./examples/count-of-each-sign.png "count-of-each-sign"
[image12]: ./examples/TrafSign_gray.png "TrafSign_gray.png"
[image13]: ./examples/5test-images.png "5test-images.png"
[image14]: ./examples/5test-images-compared.png "5test-images-compared.png"
[image15]: ./examples/input-image.png "input-image.png"
[image16]: ./examples/conv1.png "conv1.png"
[image17]: ./examples/conv2.png "conv2.png"


## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/slstoneslei/Traffic_Sign_Classifier/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing the traffic sign labels.

![traffic sign labels][image10]

Here is the count of each sign.

![count of each sign][image11]


### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale, because in cnn classification task, color infomation doesn't help much in classification, meanwhile edge information usually is more helpful. Convert the images to grayscale will speed things up and any drawbacks could be supplemented with more training data.

I use cv2.cvtColor function to accomplish this convert.

Here is an example of a traffic sign image after grayscaling.

![alt text][image12]

Secondly, I normalized the image data, because after normalization, image data have 0 mean and standard deviations, and the ranges of our distributions of feature values would likely be similar to each feature,  which can also accelerate the training process.

After normalization, i define the type of image data and image label, which set all the data have proper data type.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 gray image   							| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 32x32x32 	|
| RELU					|												|
| Convolution 3x3     	| 1x1 stride, same padding, outputs 32x32x32 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 16x16x32 				|
| Convolution 3x3     	| 1x1 stride, same padding, outputs 16x16x64 	|
| RELU					|		
| Convolution 3x3     	| 1x1 stride, same padding, outputs 16x16x64 	|
| RELU					|	
| Max pooling	      	| 2x2 stride,  outputs 8x8x64 				|
| Convolution 3x3     	| 1x1 stride, same padding, outputs 8x8x128 	|
| RELU					|	
| Convolution 3x3     	| 1x1 stride, same padding, outputs 8x8x128 	|
| RELU					|	
| Convolution 3x3     	| 1x1 stride, same padding, outputs 8x8x128 	|
| RELU					|	
| Max pooling	      	| 2x2 stride,  outputs 4x4x128 				|
| Fully connected		| 2048->256        									|
| RELU					|	
| Fully connected		| 256->43        									|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used cross entropy as cost funtion, AdamOptimizer as optimizer, the purpose of optimizer is minimize the 
cross-entropy. Learning_rate was set to be 0.001, BATCH_SIZE is 128, and EPOCHS is 20.
During training process, validation_accuracy is the performance indicators. After training process, the trained model will be saved for later use.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* validation set accuracy of 0.938
 

### Test a Model on New Images

#### 1. Choose five German traffic signs, predict their labels.

Here are five German traffic signs that I found in the test image set:

![alt text][image13] 


#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Right-of-way at the next intersection      		| Right-of-way at the next intersection   									| 
| Turn left ahead     			| Turn left ahead										|
| Children crossing					| Children crossing											|
| No vehicles      		| No vehicles				 				|
| Bumpy road		| Bumpy road      							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. 
![alt text][image14] 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.00000000e+00         			| Right-of-way at the next intersection   									| 
| 3.37956635e-10     				| Children crossing 										|
| 1.36430623e-15					| Speed limit (120km/h)											|
| 1.18945555e-16	      			| Roundabout mandatory				 				|
| 2.20503587e-17				    | Dangerous curve to the left     							|

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?
The input is random selected, the input image is 
![alt text][image15] 

First convolutional layer's output is
![alt text][image16] 

Second convolutional layer's output is
![alt text][image17] 


