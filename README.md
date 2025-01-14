# **Traffic Sign Recognition**

## Writeup

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:

- Load the data set (see below for links to the project data set)
- Explore, summarize and visualize the data set
- Design, train and test a model architecture
- Use the model to make predictions on new images
- Analyze the softmax probabilities of the new images
- Summarize the results with a written report

[//]: # "Image References"
[image1]: ./examples/visualization.png "Visualization"
[image2]: ./examples/histogram.png "Histogram"
[image3]: ./examples/grayscale.jpg "Grayscaling"
[image4]: ./test_images/ahead_only.jpg "Traffic Sign 1"
[image5]: ./test_images/caution.jpg "Traffic Sign 2"
[image6]: ./test_images/priority_road.jpg "Traffic Sign 3"
[image7]: ./test_images/right_of_way_at_next.jpg "Traffic Sign 4"
[image8]: ./test_images/stop.jpg "Traffic Sign 5"

## Rubric Points

### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used python to calculate summary statistics of the traffic
signs data set:

- The size of training set is 34799
- The size of the validation set is 4410
- The size of test set is 12630
- The shape of a traffic sign image is 32x32x3
- The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It displays an example of each traffic sign with the classification and label.

![alt text][image1]

I also created histograms which show the frequency of each ID in the training, validation, and test sets. It can be clearly that there is an uneven distribution of the different classes.

![alt text][image2]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because ...

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image3]

As a last step, I normalized the image data so that it would have mean zero and equal variance. This was accomplished by dividing all of the pixel values by 255 (grayscale max value).

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

|      Layer      |                 Description                 |
| :-------------: | :-----------------------------------------: |
|      Input      |           32x32x1 Grayscale image           |
| Convolution 5x5 | 1x1 stride, valid padding, outputs 28x28x16 |
|      RELU       |                                             |
|   Max pooling   |        2x2 stride, outputs 14x14x16         |
| Convolution 5x5 | 1x1 stride, valid padding, outputs 10x10x32 |
|      RELU       |                                             |
|   Max pooling   |         2x2 stride, outputs 5x5x32          |
| Fully connected |  input 800 (5x5x32 flattened), outputs 400  |
|      RELU       |                                             |
| Fully connected |           input 400, outputs 300            |
|      RELU       |                                             |
| Fully connected |            input 300, outputs 43            |

#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Adam Optimizer with a batch size of 128 for 50 epochs and a learning rate of 0.001.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:

- train set accuracy of 0.996 (Calculated in 'Train the Model' block)
- validation set accuracy of 0.938 (Calculated in 'Train the Model' block)
- test set accuracy of 0.942 (Calculated in 'Evaluate the Model' block)

I based my model upon the LeNet convolutional neural network architecture. I started out with default configuration for the LeNet - using RBG inputs depths of 8 and 16 for the convolutions. This performed reasonably well and I was able to achieve an accuracy of 0.89 on the validation set.

To reach the necessary threshold of 0.93, I first converted the images to grayscale. This gave me a small improvement, but it was still not enough to reach the threshold of 0.93. Next, I doubled the depth of both convolutions to 16 and 32 layers. This had the added benefit of increasing the number of inputs into the fully connected layers. To process the additional parameters, I increased the epochs to 50. With these changes I was able to achieve an accuracy of 0.942 on the test set.

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6]
![alt text][image7] ![alt text][image8]

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

|             Image              |           Prediction           |
| :----------------------------: | :----------------------------: |
|           Ahead only           |           Ahead only           |
|        General caution         |        General caution         |
|         Priority road          |         Priority road          |
| Right-of-way next intersection | Right-of-way next intersection |
|              Stop              |              Stop              |

The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 94%.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 'Predict the Sign Type for Each Image' block.

For the first image, the model is very sure that this is a priority road (probability of 1.0), and the image does contain a priority road. The top five soft max probabilities were

| Probability |      Prediction      |
| :---------: | :------------------: |
|   1.0000    |    Priority Road     |
|   0.0000    |        Yield         |
|   0.0000    |      Ahead only      |
|   0.0000    |     No vehicles      |
|   0.0000    | Roundabout mandatory |

For the second image ...

| Probability |      Prediction      |
| :---------: | :------------------: |
|   1.0000    |      Ahead only      |
|   0.0000    |      Road work       |
|   0.0000    |    Priority Road     |
|   0.0000    |        Yield         |
|   0.0000    | Go straight or right |

For the third image...

| Probability |     Prediction     |
| :---------: | :----------------: |
|   0.9994    |        Stop        |
|   0.0004    | Speed limit 70km/h |
|   0.0000    |     No passing     |
|   0.0000    |    No vehicles     |
|   0.0000    |       Yield        |

For the fourth image...

| Probability |            Prediction             |
| :---------: | :-------------------------------: |
|   1.0000    | Right of way at next intersection |
|   0.0000    |        Beware of ice/snow         |
|   0.0000    |           Double curve            |
|   0.0000    |            Pedestrians            |
|   0.0000    |          General caution          |

For the fifth image...

| Probability |            Prediction             |
| :---------: | :-------------------------------: |
|   1.0000    |          General caution          |
|   0.0000    | Right of way at next intersection |
|   0.0000    |            Pedestrians            |
|   0.0000    |        Speed limit 20km/h         |
|   0.0000    |       Roundabout mandatory        |

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)

#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?
