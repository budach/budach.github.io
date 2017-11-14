# Class Model - Documentation

The Model class represents a convolutional neural network and provides functions for network training and visualization of learned features (sequence/structure motifs). The basic structure of the network consists of a variable number of convolutional and max pooling layers followed by a variable number of dense layers. These layers are interspersed by dropout layers after the input layer and after every max pooling and dense layer. The network can be tuned using the following hyperparameters which can be provided through the 'params' parameter of the \_\_init\_\_ function: 

  | parameter | default | description |  
  |:-|:-|:-|  
  | conv\_num | 2 | number of convolutional/pooling layers |  
  | kernel\_num | 50 | number of kernels in each conv layer |  
  | kernel\_len | 25 | length of kernels |  
  | pool\_size | 2 | size of pooling windows |  
  | pool\_stride | 2 | step size of pooling operation |  
  | dense\_num | 1 | number of dense layers |  
  | neuron\_num | 100 | number of neurons in each dense layer |  
  | dropout\_input | 0.1 | dropout portion after input |  
  | dropout\_conv | 0.4 | dropout portion after pooling layers |  
  | dropout\_dense | 0.4 | dropout portion after dense layers |  
  | batch\_size | 256 | batch size during training |  
  | learning\_rate | 0.0005 | learning rate of Adam optimizer |  
  | patience\_lr | 5 | number of epochs without validation loss improvement before halving the learning rate |  
  | patience\_stopping | 15 | number of epochs without validation loss improvement before stopping the training |  
  | epochs | 500 | maximum number of training epochs |  
  | kernel\_constraint | 3 | max-norm weight constraint |  
 

 Not all parameters are equally important when doing a hyperparameter grid search. The ones with a big influence are usually conv\_num (range 1-3), kernel\_num (range 50-300), neuron\_num (50-1000) and the dropout parameters (around 0.1 for the input and 0.2-0.6 otherwise).

## Methods - Overview

| name | description |
|:-|:-|
