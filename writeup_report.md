# **Behavioral Cloning** 

## Writeup 
---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* Beh_Clon.ipynb containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```
The vehicle longitudinal velocity was set to 30 mph.

#### 3. Submission code is usable and readable

The Beh_Clon.ipynb file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. Preprocessing of the training images was done in order to focus model on the important features 

The training images are first normalized and mean centred using Lambda function of Keras. This procedure ist followed by Cropping2D function that provide the model only the relevant area of the image by cropping out the upper part with landscape and lower part depicting the car hood.  

#### 2. The used CovNet Architecture 

After several attempts with LeNet and its adaptation i decided to use the nVidia Architecture. I received best results when using the NVIDIA architecture with added dropout layers.

![CovNet Model] (https://raw.githubusercontent.com/mikaspar/CarND_Term1_Behavioral_Cloning/master/model_plot.png)

The model was trained and validated on different data sets to ensure that the model was not overfitting (using validation_split =0.2 of Keras fit function). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road using the offroad training data. To improve the ability of the vehicle to keep in the centre of the road i used the left and right camera images. The steering angle for these cameras were corrected by 0.09 degrees. In order to avoid vehicle to prefer (overfit) the left turn were all images and corresponding steering angles mirrored.    
 
At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

### Challenge track

To keep the vehicle on the road of the challenge track it was necessary to provide additional training data from this track and to reduce the longitudinal speed to 10 mph. The finetuning on this track was not finished on the dead line date.
