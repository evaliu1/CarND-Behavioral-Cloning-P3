# Behavioral Cloning
### Resubmit version

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

My first step was to use a Cropping method to just keep the road part. Then I resized my image to 66-200-3, used Lambda function to normalize the image. 
After that I applied Convolution Neural network to process the image.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I also used generator function to save the storage. 

The final step was to run the simulator to see how well the car was driving around track one. At the beginning, the car would drive out of the track, so I increased the epoch number to get a better performance.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture consisted of a convolution neural network with the following layers and layer sizes.


| Layer (type)   |                  Output Shape     |     Param #   |  Connected to |
|:-----------------------------:|:------------------------------:|:-----------------:|:---------------------------------------:| 
|cropping2d_1 (Cropping2D)   | (None, 80, 320, 3)  |  0    |     cropping2d_input_1[0][0]  |        
|lambda_1 (Lambda)     | (None, 66, 200, 3)   |  0    |     cropping2d_1[0][0]      |         
|lambda_2 (Lambda)     | (None, 66, 200, 3)    |  0    |     lambda_1[0][0]           |       
|convolution2d_1 (Convolution2D)|  (None, 33, 100, 24) |   1824  |     lambda_2[0][0]           | 
|spatialdropout2d_1 (SpatialDrop)| (None, 33, 100, 24)|   0       |   convolution2d_1[0][0]     |
|convolution2d_2 (Convolution2D)| (None, 17, 50, 36) |   21636   |    convolution2d_1[0][0]    | 
|spatialdropout2d_2 (SpatialDrop)| (None, 17, 50, 36) |   0       |    convolution2d_2[0][0]    |
|convolution2d_3 (Convolution2D) | (None, 7, 23, 48)  |   43248   |    spatialdropout2d_2[0][0] |
|spatialdropout2d_3 (SpatialDrop)| (None, 7, 23, 48)  |    0     |      convolution2d_3[0][0]   |
|convolution2d_4 (Convolution2D) | (None, 5, 21, 64)  |   27712  |    spatialdropout2d_3[0][0] |
|spatialdropout2d_4 (SpatialDrop)| (None, 5, 21, 64)  |   0      |     convolution2d_4[0][0]   |
|convolution2d_5 (Convolution2D) | (None, 3, 19, 64)  |  36928   |    spatialdropout2d_4[0][0] |
|spatialdropout2d_5 (SpatialDrop)| (None, 3, 19, 64)  |   0       |    convolution2d_5[0][0]   |
|flatten_1 (Flatten)        | (None, 3648)      |    0       |    spatialdropout2d_5[0][0] |
|activation_1 (Activation)  | (None, 3648)      |    0       |    flatten_1[0][0]         |
|dense_1 (Dense)       | (None, 100)  |     364900 |     activation_1[0][0]      |
|activation_2 (Activation)| (None, 100)|    0   |        dense_1[0][0]    |
|dense_2 (Dense)      | (None, 50) |    5050  |      activation_2[0][0]  |
|activation_3 (Activation)| (None, 50) |    0   |      dense_2[0][0]  |
|dropout_1 (Dropout)  | (None, 50)  |   0     |    activation_3[0][0]|   
|dense_3 (Dense)      | (None, 1)   |   51    |     dropout_1[0][0] |



#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I used 7 tracks of training set.

1. Three full tracks for center road driving

2. One track of driving side recovery 

3. One track of turning around, driving the other way of the track

4. Two subtracks of turning record

Here is an example image of center lane driving:

![alt text](https://github.com/evaliu1/CarND-Behavioral-Cloning-P3/blob/master/Img/center_2016_12_01_13_30_48_287.jpg)


After the collection process, I had 30485 number of data points. I then preprocessed this data using pre-defined generator function. I finally randomly shuffled the data set and put 1605 data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. I used 20 epoch to train the data. And I got the training loss for 0.0457.

I used an adam optimizer and set the learning rate as 0.01.

Then I simulated my model and recorded the driving video.

![video demo](https://github.com/evaliu1/CarND-Behavioral-Cloning-P3/blob/master/run1.mp4)


