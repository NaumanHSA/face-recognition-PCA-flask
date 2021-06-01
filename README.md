# Introduction

This is Face Recognition web application developed using Flask API. The application have three main modules which are: 

1. The Registration Module
2. The Training module
3. The Recognition module

The flow of the application is something like:

- A user is first registered with either of the following two ways. First, by choosing his images which are stored somewhere locally. Second, a user can be registered by running live webcam in case he's present physically. The camera will take specified number of images and register the person.

- After taking photos of a user to be regisrered, a user can recognise the registered person by clicking on the recognise button which will open webcam.

# How Algorithm Works

The face recognition is performed using Principle Component Analysis aka PCA. A deep learning algorithm called MTCNN is used to frist detect faces in an image. The face is aligned using left and right eyes locations, converted into grey-scal image, cropped and then saved under particular person name's folder. 

PCA is a technique which is used the reduce a highly dimensional data into simple form keeping the most of information. For example, in our code we have face images of 64x64, when flatten it makes a single image with 4096 features. We have performed the PCA and chosen the first 51 principle components. Before performing PCA, we generate a mean-face for every person by taking mean of all samples for one particular person.

After PCA, we take a test image which is unseen to the algorithm, perfrom the same PCA on it and then compare the two arrays by computing L2 norm distance (eucledean distance). We then compare the distance with a certain threshold and recognize a person as one of the known people or unknown person.


# How to set up the Environment:

Install all necessary libraries by running the following command:

    pip install -r requirements.py


# How to run the code:

The code can be run with cmd command with some flags to specify which are user's choice. The flags description are:

- **--training_images:** # of images required to train the classifier on, greater number brings better accuracy, default is 10.

- **--distance_threshold:** How much distance between faces to consider it a match. Lower is more strict. 0.5 is typical best performance.

- **--resize_scale:** Resize the input video, e.g. 0.75 will resize to 1/4th of the video. default is 1 means No resize.

A sample command for running the app can be like:

    python run.py --training_images=10 --gpu --resize_scale=0.75

You can then visit http://localhost:5000/ to view the website. Thanks !!!