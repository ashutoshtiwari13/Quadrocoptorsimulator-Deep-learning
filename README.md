## Quadrocopter - Robotics follow me Project

A deep neural network to identify and track a target (person) via a simulated Quadrocopter (Simulated using Udacity QuadSim by Unity). Applications like these are key to many fields of robotics and the very same techniques are used for tasks of advanced cruise control in UAV's , autonomous vehicles and human-robot collaboration in the industry.

<p align="center">
  <img src="https://github.com/ashutoshtiwari13/Quadrocoptorsimulator-Deep-learning/blob/master/quadsim_simulation.gif" width="750px" height="400px"/></p>

### Project Details
 - [Network Architecture](#Network-Architecture)
 - [Project Setup](#Project-Setup)
 - [Run Simulation](#Run-Simulation)

## Network Architecture
A full convolution network(FCN) is used to train the semantic segmentation model. It contains three encoder blocks, a 1x1 convolution layer, and three symmetrical decoder blocks.

FCN's have earlier achieved state-of-the-art results in semantic segmentation tasks by making use of the follwoing techniques also a part of the network architecture of the project,
 - 1x1 convolutional layer instead of fully connected layers (since the fully connected layer cannot preserve spatial information which is a must in the project)
 - Upsampling , via a customized BilinearUpsampling2D (implemented in utils.separable_conv2d), of the decoder
 - Skip connection , which allow the network to use information from multiple resolution scales and helps to make more precise segmentation decisions.

 Note : Though state-of-the-art models like **YOLO** and **SSD** perform extremely well at high frames per second but the generated bounded boxes can only provide partial seen understanding and so the need of **Semantic segmentation** in the project arises.

### Hyperparameters

```
learning_rate = 0.01
batch_size = 15
num_epochs = 60
steps_per_epoch = 200
validation_steps = 50
workers = 2

```
With these hyper-parameter settings above, it took 6-7 hours to train the model on collab.

## Project Setup

### Dependencies
- Uses the Udacity-RoboND Quadsim Simulator made with Unity, details of which can be found [here](https://github.com/udacity/RoboND-DeepLearning-Project/releases/tag/v1.2.2)
- Python 3.5+ (Project uses Py3.5 keeping in mind the corresponding RoboND-QuadSim)
- Install other dependencies using ,
```sh
$ pip install -r requirements.txt
```

### Image data
The image data(Training Data, Validation Data, Sample Evaluation Data) can be found in the ```data``` directory in the cloned repository by ,

```sh
$ git clone https://github.com/ashutoshtiwari13/Quadrocoptorsimulator-Deep-learning.git
```

## Run Simulation
1. Details of the network implementation,training and precision is present in the jupyter-notebook ```drone_sim_dl.ipynb```.
2. Save your trained model from the above training in the weights directory ( ```data/weights```).
3. Launch the simulator , select "Spawn People" followed by "Follow Me" button.
4. Run the following ,

```sh
$ python follower.py --pred_viz <your_trained_model>.h5
```
