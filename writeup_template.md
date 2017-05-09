**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Images/placeholder.png "Model Visualization"
[image1]: ./Images/image1.png "Center Image"
[image3]: ./Images/LeftImg1.png "Left recovery Image"
[image4]: ./Images/CenterImg1.png "Center Image"
[image5]: ./Images/RightImg1.png "Right recovery Image"
[image6]: ./Images/Image_BeforeFlip.png "Normal Image"
[image7]: ./Images/Image_AfterFlip.png "Flipped Image"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
###Files Submitted & Code Quality

####1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results

####2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

####3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

###Model Architecture and Training Strategy

####1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 3x3 filter sizes and depths between 32 and 128 (model.py lines 18-24) 

The model includes RELU layers to introduce nonlinearity (code line 20), and the data is normalized in the model using a Keras lambda layer (code line 18). 

####2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.py lines 21). 

The model was trained and validated on different data sets to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

####3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 25).

####4. Appropriate training data

I chose udacity's data as it's better what i was able to record.To simulate the recovery data, i added left and right images with a steering angle correction of 0.25.

For details about how I created the training data, see the next section. 

###Model Architecture and Training Strategy

####1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the Nividia model as its known and tested model for self driving cars.This model is appropriate as i am trying to simulate the car to drive in autonomous mode.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model so that large number of data is used for training by implementing keras generator.
I also used data augmentation techniques which included changing brightness, adding random shadow,transforming image by horizontal/vertical shift and randomly flipping the image.

The final step was to run the simulator to see how well the car was driving around track one. 

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

####2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project rubric)

![alt text][image1]

####3. Creation of the Training Set & Training Process

I have used udacity's training data and a sample center image is shown as 

![alt text][image2] Image1

To simulate the recovery data, added left image with steering correction of 0.25 and right image with -0.25:

![alt text][image3]
![alt text][image4]
![alt text][image5]


To augment the data set, I also flipped images and angles thinking that this would simulate driving in opposite direction. For example, here is an image that has then been flipped:

![alt text][image6]
![alt text][image7]

Also i added horizontal shift to simulate the car being on different positions of the road.And added vertical shifts at random to simulate the driving on slope up and down.

Data set was finally split and 20% is used for validation set.I used a keras generator to have large training data, where 20000 number of samples was used for each epoch and 800 validation samples per epoch. After 3 epochs, i was satisfied that loss i minimum and both validation and training loss converged.So i used this model to run in autonomous mode on track1.Though the car speed is at 9pmh, the ride was smoother and did pretty well.


