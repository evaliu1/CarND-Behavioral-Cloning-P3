# Behavioral Cloning

### Eva Liu
Behavioral Cloning Project

The goals / steps of this project are the following:

Use the simulator to collect data of good driving behavior
Build, a convolution neural network in Keras that predicts steering angles from images
Train and validate the model with a training and validation set
Test that the model successfully drives around track one without leaving the road
Summarize the results with a written report
Rubric Points


### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to use LetNet architecture to train the driving data. Then valid my data using valid data set. 

My first step was to use a Cropping method to just keep the road part. Then I resized my image to 16-32-3, used Lambda function to normalize the image. 
After that I applied Convolution Neural network to process the image.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I also used generator function to save the storage. 

The final step was to run the simulator to see how well the car was driving around track one. At the beginning, the car would drive out of the track, so I increased the epoch number to get a better performance.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture consisted of a convolution neural network with the following layers and layer sizes.


| Layer (type)   |                  Output Shape     |     Param #   |  Connected to |
|:-----------------------------:|:------------------------------:|:-----------------:|:---------------------------------------:| 
|cropping2d_1 (Cropping2D)   |     (None, 65, 320, 3)  |  0    |     cropping2d_input_1[0][0]  |        
|lambda_1 (Lambda)     |           (None, 16, 32, 3)   |  0    |     cropping2d_1[0][0]      |         
|lambda_2 (Lambda)     |          (None, 16, 32, 3)    |  0    |     lambda_1[0][0]           |       
|convolution2d_1 (Convolution2D)|  (None, 14, 30, 16) |   448  |     lambda_2[0][0]           |       
|convolution2d_2 (Convolution2D)|  (None, 12, 28, 32) |   4640   |    convolution2d_1[0][0]    |        
|convolution2d_3 (Convolution2D)|  (None, 10, 26, 64) |   18496  |    convolution2d_2[0][0]     |       
|maxpooling2d_1 (MaxPooling2D) |   (None, 5, 13, 64)  |   0      |    convolution2d_3[0][0]      |     
|dropout_1 (Dropout)         |     (None, 5, 13, 64)  |   0      |    maxpooling2d_1[0][0]      |       
|flatten_1 (Flatten)         |    (None, 4160)        |   0       |    dropout_1[0][0]           |       
|activation_1 (Activation)   |   (None, 4160)        |   0        |    flatten_1[0][0]            |      
|dense_1 (Dense)             |     (None, 100)       |   416100  |    activation_1[0][0]       |        
|activation_2 (Activation)   |     (None, 100)       |   0        |  dense_1[0][0]              |      
|dense_2 (Dense)             |     (None, 50)        |   5050    |    activation_2[0][0]         |      
|activation_3 (Activation)   |     (None, 50)        |   0       |    dense_2[0][0]              |      
|dense_3 (Dense)             |     (None, 1)         |   51      |    activation_3[0][0]   |

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I used the given data.zip file as my input data (I couldn't control the car going straight using simulator). Here is an example image of center lane driving:

![alt text](https://github.com/evaliu1/CarND-Behavioral-Cloning-P3/blob/master/Img/center_2016_12_01_13_30_48_287.jpg)


After the collection process, I had 7634 number of data points. I then preprocessed this data using pre-defined generator function.

I finally randomly shuffled the data set and put 402 data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. I used 15 epoch to train my data. And I got the data loss as 0.0059, validation loss as 0.0079.

I used an adam optimizer so that manually training the learning rate wasn't necessary.
