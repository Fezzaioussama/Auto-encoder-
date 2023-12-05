# Autoencoder Models for MNIST Dataset

This repository contains the implementation of autoencoder models for the MNIST dataset. Two types of autoencoders, namely Linear Autoencoder and Convolutional Autoencoder, have been developed and evaluated.

## Overview

Autoencoders are a class of neural networks used for unsupervised learning. They aim to learn a compressed, low-dimensional representation of input data and then reconstruct the input data from this representation. In this work, we explore the use of autoencoders for the MNIST dataset, which consists of grayscale images of handwritten digits.

## Models Implemented

### 1. Linear Autoencoder

The Linear Autoencoder is a basic architecture composed of fully connected layers. It encodes the input image into a lower-dimensional latent space and then decodes it back to the original dimension. The purpose is to learn a meaningful representation of the input data.
### 2. Convlutional Autoencoder
The Convolutional Autoencoder extends the basic architecture by incorporating convolutional layers. Convolutional layers are effective in capturing spatial patterns in images. This model aims to learn hierarchical features of the input images through convolutional operations.
