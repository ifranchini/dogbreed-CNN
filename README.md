# dogbreed-CNN 
Dog breed classification using Transfer learning and Convolutional Neural Networks (CNN). This project was done as part of the Udacity Deep Learning nanodegree program.

## Overview

The goal of this project is to apply the knowledge gained on how to create a CNN from scratch and then train it to recognize dog breeds from an image. After my initial attempt at building a simple CNN network, transfer learning will be used to improve the network's predictions and increase the accuracy of the recognized breeds. Addictionally, `open-cv` is used to detect faces in images and I'll be using the network to determine what that human looks like (in terms of dog breeds) :satisfied:

## Methodology

Outlined below are the high level steps I used. Important to remark that PyTorch and OpenCV were used for the entire project

1. Prepare datasets
    - Download the [dog dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip) and add it to the  root folder of your project (`/dogImages`)
    - Download the [human dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/lfw.zip) (`/lfw`)
    - Get the full classes dictionary from [ImageNet](https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a) to associate class index with breeds
    - Prepare training, test and validation batches, making sure to augment your training data to avoid overfitting

2. Building CNN
    - First I'll use a simple CNN architechture, using 3 CNN layers for feature detection and 3 fully connected MLP to classify the images. This network has a low accuracy, but it's important to understand how different architecture choices and hyperparameter settings affect the result of your network
    - After this attempt I use transfer learning using the pretrained VGG16 model. The feature detection layers will be used as they come and I will focus on training the classifier layers, changing the last fully connected layer in order to fit our target case.
    - Setup optimization, loss function and related hyperparameters in order to achieve better results

3. App development
    - Using the newly trained network along with OpenCV for face recognition, I built a function that takes as input a path to an image and returns:
        - Results if a human face or a dog was detected
        - Apply model in order to predict dog breed or human-dog resemblance
        - If no faces or dogs found in image, do nothing

## Tools 

For this project I used an [AWS Deep Learning AMI (Ubuntu 18.04)](https://aws.amazon.com/marketplace/pp/Amazon-Web-Services-AWS-Deep-Learning-AMI-Ubuntu-1/B07Y43P7X5). I highly recommend using [VS Code](https://code.visualstudio.com/) and remote-SSH into your instance (Make sure you have a security group that allows port 22 from your IP). I worked in `pytorch_latest_p37` virtual env that comes with the forementioned instance, which already contains the libs `open-cv` and `pytorch`