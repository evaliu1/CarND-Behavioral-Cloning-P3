# Behavioral Cloning

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

My first step was to use a convolution neural network model similar to the ... I thought this model might be appropriate because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting.

To combat the overfitting, I modified the model so that ...

Then I ...

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track... to improve the driving behavior in these cases, I ....

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project rubric)

| Layer (type)   |                  Output Shape     |     Param #   |  Connected to |
|:---------------------:|:-------------------------------------:|:-----------------:|:---------------------------------------------:| 
cropping2d_1 (Cropping2D)   |     (None, 65, 320, 3)  |  0    |       cropping2d_input_1[0][0]  |        
lambda_1 (Lambda)     |           (None, 16, 32, 3)   |  0    |      cropping2d_1[0][0]      |         
lambda_2 (Lambda)     |          (None, 16, 32, 3)    | 0    |       lambda_1[0][0]           |       
convolution2d_1 (Convolution2D)|  (None, 14, 30, 16) |   448  |       lambda_2[0][0]           |       
convolution2d_2 (Convolution2D)|  (None, 12, 28, 32) |   4640   |     convolution2d_1[0][0]    |        
convolution2d_3 (Convolution2D)|  (None, 10, 26, 64) |   18496  |    convolution2d_2[0][0]     |       
maxpooling2d_1 (MaxPooling2D) |   (None, 5, 13, 64)  |   0      |   convolution2d_3[0][0]      |     
dropout_1 (Dropout)         |     (None, 5, 13, 64)  |   0      |    maxpooling2d_1[0][0]      |       
flatten_1 (Flatten)         |    (None, 4160)        |  0       |    dropout_1[0][0]           |       
activation_1 (Activation)   |   (None, 4160)        |  0        |   flatten_1[0][0]            |      
dense_1 (Dense)             |     (None, 100)       |    416100  |    activation_1[0][0]       |        
activation_2 (Activation)   |     (None, 100)       |   0        |  dense_1[0][0]              |      
dense_2 (Dense)             |     (None, 50)        |    5050    |  activation_2[0][0]         |      
activation_3 (Activation)   |     (None, 50)        |   0        |  dense_2[0][0]              |      
dense_3 (Dense)             |     (None, 1)         |    51      |  activation_3[0][0]   |

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

alt text

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to .... These images show what a recovery looks like starting from ... :

alt text alt text alt text

Then I repeated this process on track two in order to get more data points.

To augment the data sat, I also flipped images and angles thinking that this would ... For example, here is an image that has then been flipped:

alt text alt text

Etc ....

After the collection process, I had X number of data points. I then preprocessed this data by ...

I finally randomly shuffled the data set and put Y% of the data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was Z as evidenced by ... I used an adam optimizer so that manually training the learning rate wasn't necessary.
