# Face Recognition in Action 

## Introduction

In the last few decades, the research on face recognition has become a trendy topic. Significant developments have been made by various research in this field. The definition of face recognition can be expressed as a task using biometric features to recognize the human face. The tasks of face recognition can be divided into three types: Face verification (are they the same person), face identification (who is this person), and face clustering (find common people among these faces). 

To check what we have learned in this semester, we decided to train a face verification model in a real-world dataset with deep learning approaches. The dataset we used is the Labeled Faces in the Wild Database (LFW). The LFW database is a well-known in face recognition field. It contains more than 13,000 images of faces collected from the web. Each face has been labeled with the name of the person in the picture. There are 1,680 individuals have two or more distinct photos in the dataset. 

Our method followed the general machine learning workflow: starting with data preprocessing, building model from baseline then improving the model step by step to gain a better performance on the test data.

This project aims to train a deep learning model for face verification task. Similar to other machine learning tasks, our method is a purely data driven method as the faces are represented by the pixels. The deep learning network we used is the convolutional neural network. Although face recognition model has been developed very sophisticated, our project is proposed to check the deep learning knowledge we have learnt in this semester. Thus, this project can be regard as a deep learning model training for face recognition in action. With limited computational power, we managed to adjust the model to its best performance.

## Data

The database we used is the Labeled Faces in the Wild (LFW), a database of face photographs designed for studying the problem of unconstrained face recognition. Unconstrained means that the images in it are random images that all the elements in them can variate, from pose to emotion, from angle to lighting. The LFW dataset has a pre-defined subset for development purpose, which has 2,200 training pairs and 1,000 test pairs. Our approach followed this training and test data split. 

The LFW dataset has its own pre-processing methods: funnel and deep funnel. This pre-processing is applied to original data by rotating and resizing to ensure every image has a similar eye and nose position and the faces are at the center of the image. 

One of the drawbacks of this dataset is that it is not a big training dataset to train a model with good performance. To feed a deep learning model with high accuracy, more data is needed. Instead, the LFW dataset is a frequently used benchmark testing dataset for face recognition. 

## Method 


Our model used deep convolutional network. The face recognition task always starts with a data preparation for face alignment. We used the pre-processed data from the LFW dataset: the deep funneled faces. These deep funneled faces kept the eye and nose position of every image at the same position which can help with the performance of face recognition task. 
Our own data preparation started with cropping. The original image in the LFW dataset has a size of 250 by 250 pixels. We cropped the surrounding pixels of the image, left the center of the image which lies the faces. It caused a decreasing of image size from 250 by 250 to 128 by 128 pixels. 

**Cropping:**

![pic1](https://github.com/ZhenghaoXiao32/Face-Recognition-in-Action-LFW/blob/master/pics/Picture1.png)

After cropping, we applied a down-sampling to the image. It reduced the image size from 128 by 128 pixels to 32 by 32 images. The reason of applying down-sampling is to reduce the computational power required to train the model. Figure 3 shows the procedure of down-sampling. In addition to these image pre-processing, we also linked the names of people with their images.

**Down-sampling:**

![pic2](https://github.com/ZhenghaoXiao32/Face-Recognition-in-Action-LFW/blob/master/pics/Picture2.png)

The main task of our model is to detect if the faces in a pair of images are of the same person. If a pair of images contains the same person, we call it a matched pair, otherwise, it is a mismatched one. 

**Pairs:**

![pic3](https://github.com/ZhenghaoXiao32/Face-Recognition-in-Action-LFW/blob/master/pics/Picture3.png)

For model building, firstly, we picked up a baseline model from [charlesreid1/in-your-face](https://github.com/charlesreid1/in-your-face). Two convolutional layers were applied with a 3 by 3 filter size, dropouts were applied to reduce overfit. The baseline model was training with 25 epochs and a batch size of 128, achieved an 70.3% accuracy in test data. After exploring the different convolution layer size based on the baseline model, we built the complex model with a more complicated layer setting. 

## Results and Discussion

We experimented batch size of 32, 64, and 128 on the complex model, and applied the callback of the best performance model. The final model used 128 as the batch size, 100 epochs, gained a 72.8% accuracy on the test data. 

The performance of the model is fair, but we can still improve the model by advancing the network structure, increasing the input size of the images, and by deploying cloud computation to get more computational power.

We also reviewed the advanced model: FaceNet by google. One possible way to improve the performance is to accommodate their inception structure in our layers. However, this method is highly computational power demanding. We may switch to cloud computation platforms for achieve this goal in the future. 

## Required Packages for Data Importing

* [fuel](https://github.com/mila-iqia/fuel)
* [kerosene](https://github.com/dribnet/kerosene)
* [lfw_fuel](https://github.com/dribnet/lfw_fuel)

Deprecated requirements were adjusted.

## License
The contents of this repository are covered under the [MIT License](LICENSE).
