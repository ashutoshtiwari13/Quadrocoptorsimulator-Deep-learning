## Quadrocopter - Robotics follow me Project

A deep neural network to identify and track a target (person) via a simulated Quadrocopter (Simulated using Udacity QuadSim by Unity). Applications like these are key to many fields of robotics and the very same techniques are used for tasks of advanced cruise control in UAV's , autonomous vehicles and human-robot collaboration in the industry.

![Simulation Image]()
### Project Details
 - [Network Architecture](#Network-Architecture)
 - [Project Setup](#Setup)
 - [Dependencies](#Dependencies)

## Network Architecture
A full convolution network(FCN) is used to train the semantic segmentation model. It contains three encoder blocks, a 1x1 convolution layer, and three symmetrical decoder blocks.

FCN's have earlier achieved state-of-the-art results in semantic segmentation tasks by making use of the follwoing techniques also a part of the network architecture of the project,
 - 1x1 convolutional layer instead of fully connected layers (since the fully connected layer cannot preserve spatial information which is a must in the project)
 - Upsampling , via a customized BilinearUpsampling2D (implemented in utils.separable_conv2d), of the decoder
 - Skip connection , which allow the network to use information from multiple resolution scales and helps to make more precise segmentation decisions.

 Note : Though state-of-the-art models like **YOLO** and **SSD** perform extremely well at high frames per second but the generated bounded boxes can only provide partial seen understanding and so the need of **Semantic segmentation** in the project arises.

### Hyperparamters

```
learning_rate = 0.01
batch_size = 15
num_epochs = 60
steps_per_epoch = 200
validation_steps = 50
workers = 2

```

## Project Setup

## Dependencies
