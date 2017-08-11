**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Images/model.png "Model Visualization"
[image2]: ./Images/Image1.png "Center Image"
[image3]: ./Images/RecoveryImg.png "Recovery Image"
[image4]: ./Images/FlipImage.png "Flip Image"

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results

**1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 5x5 filter sizes and depths between 24 and 68 (model.py lines 104-123).There are 5 concolutionals layers followed by 4 fully connected layers. 

I used ELU activation to introduce nonlinearity and the data is normalized using keras lamda layer (code line 108).Also i used cropping layer (code line 106) to resize input images (both training and validation data).

**2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.py lines 118 and line 120). 

The model was trained and validated on different data sets to ensure that the model was not overfitting (code line 130). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

**3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 125).

**4. Appropriate training data

I chose udacity's data as it's better what i was able to record.To simulate the recovery data, i added left and right images with a steering angle correction of 0.25.

For details about how I created the training data, see the next section. 

**Model Architecture and Training Strategy

**1. Solution Design Approach

My first step was to use a convolution neural network model similar to the Nividia model as its known and tested model for self driving cars.This model is appropriate as i am trying to simulate the car to drive in autonomous mode.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model so that large number of data is used for training by implementing keras generator.
I also used data augmentation techniques which included changing brightness,transforming image by horizontal/vertical shift and randomly flipping the image.

The final step was to run the simulator to see how well the car was driving around track one. 

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

**2. Final Model Architecture

The final model architecture (model.py lines 104-123) consisted of a convolution neural network with the following layers and layer sizes.

![alt text][image1]

**3. Creation of the Training Set & Training Process

I have used udacity's training data and a sample center image is shown as 

![alt text][image2]

To simulate the recovery data, added left image with steering correction of 0.25 and right image with -0.25:

![alt text][image3]


To augment the data set, I also flipped images and angles thinking that this would simulate driving in opposite direction. For example, here is an image that has then been flipped:

![alt text][image4]

Also i added horizontal shift to simulate the car being on different positions of the road.And added vertical shifts at random to simulate the driving on slope up and down.

Data set was finally split and 20% is used for validation set.I used a keras generator to have large training data, where 20000 number of samples was used for each epoch and 800 validation samples per epoch. After 3 epochs, i was satisfied that loss is minimum and both validation and training loss converged.So i used this model to run in autonomous mode on track1.Though the car speed is at 9pmh, the ride was smoother and did pretty well.


