# Image-Colorization
The task is to use a convolutional neural network for image colorization which turns a grayscale image to a colored image.
By converting an image to grayscale, we loose color information, so converting a grayscale image back to a colored version 
is not an easy job.

## Dataset
The CIFAR-10 dataset consists of 60000 32x32 color images in 10 classes, with 6000 images per class. There are 50000 
training images and 10000 testing images. The dataset is divided into five training batches and one test batch, 
each with 10000 images. The test batch contains exactly 1000 randomly-selected images from each class. 
The training batches contain the remaining images in random order, but some training batches may contain more images from 
one class than another. Between them, the training batches contain exactly 5000 images from each class. 

## K-Means Clustering to find Main Colors
There are total 6000 images of 32x32 dimension. So, there are P = 6000x32x32 = 6144000 pixels, each pixel having 3 channels 
(RGB vaue). Run K-means clustering on P pixels to find K = 24 clusters. The centers of the cluster will be the main colors.
Convert the colored images to K-color images by converting each pixel's value to the closest main color in terms of 
Euclidean distance. These are the outputs of the network, whose each pixel falls in one of those K clusters.

## Convolutional Neural Network (CNN) to Color Grayscale Images
Convert the original 32x32x3 images to grayscale 32x32x1 images. The grayscale images are inputs of the network. 
Set up a convolutional neural network with two convolution layers and two Multi-layer Perceptron (MLP) layers. Use max-pooling
after each convolutional layer. Use 5x5 filters and a softmax output layer. The task is to use a classification scheme, which
means the output must determine one of the K = 24 color classes for each pixel in the grayscale image. The input is a 
grayscale version of an image (32x32x1) and the output is 32x32x24. The output assigns one of the K = 24 colors to each of 
the 32x32 pixels; therefore, each of the pixels is classified into one of the K one-hot encoding classes. After each pixel is 
classified into one of the K main colors, the RGB code of that color can be assigned to the pixel. 


