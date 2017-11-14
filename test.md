# Class Model - Documentation

The Model class represents a convolutional neural network and provides functions for network training and visualization of learned features (sequence/structure motifs). The basic architecture of the network consists of a variable number of convolutional and max pooling layers followed by a variable number of dense layers. These layers are interspersed by dropout layers after the input layer and after every max pooling and dense layer. The network can be tuned using the following hyperparameters which can be provided through the 'params' parameter of the \_\_init\_\_ function: 

  | parameter | default | description |  
  |:-|:-|:-|  
  | conv\_num          | 2 | number of convolutional/pooling layers |  
  | kernel\_num        | 50 | number of kernels in each conv layer |  
  | kernel\_len        | 25 | length of kernels |  
  | pool\_size         | 2 | size of pooling windows |  
  | pool\_stride       | 2 | step size of pooling operation |  
  | dense\_num         | 1 | number of dense layers |  
  | neuron\_num        | 100 | number of neurons in each dense layer |  
  | dropout\_input     | 0.1 | dropout portion after input |  
  | dropout\_conv      | 0.4 | dropout portion after pooling layers |  
  | dropout\_dense     | 0.4 | dropout portion after dense layers |  
  | batch\_size        | 256 | batch size during training |  
  | learning\_rate     | 0.0005 | learning rate of Adam optimizer |  
  | patience\_lr       | 5 | number of epochs without validation loss improvement before halving learning rate |  
  | patience\_stopping | 15 | number of epochs without validation loss improvement before stopping training |  
  | epochs            | 500 | maximum number of training epochs |  
  | kernel\_constraint | 3 | max-norm weight constraint |  
 

 Not all parameters are equally important when doing a hyperparameter grid search. The ones with a strong influence are usually conv\_num (range 1-3), kernel\_num (range 50-300), neuron\_num (50-1000) and the dropout parameters (around 0.1 for the input and 0.2-0.6 otherwise).

## Methods - Overview

| name | description |
|:-|:-|
| \_\_init\_\_ | Initialize the model with the given parameters. |
| train | Train the model. |
| print\_summary | Print an overview of the network architecture. |
| predict | Get model predictions for a subset of a Data object. |
| get\_max\_activations | Get the network output of the first convolutional layer. |
| visualize\_kernel | Get a number of visualizations and an importane score for a convolutional kernel. |
## \_\_init\_\_

``` python
def __init__(self, params, data)
```
Initialize the model with the given parameters. 

 Example: providing the params dict {'conv\_num': 1, 'kernel\_num': 20, 'dropout\_input': 0.0} will set these 3 parameters to the provided values. All other parameters will have default values. A data object must be provided to infer the input shape and number of classes. 



| parameter | type | description |
|:-|:-|:-|
| params | dict | A dict containing hyperparameter values. |
| data | placeholder.Data | The Data object the model should be trained on. |
## train

``` python
def train(self, data, verbose = True)
```
Train the model. 

 The model will be trained and validated on the training and validation set provided by the Data object. 



| parameter | type | description |
|:-|:-|:-|
| data | placeholder.Data | The Data object the model should be trained on. |
| verbose | bool | If True, progress information will be printed throughout the training. |
## print\_summary

``` python
def print_summary(self)
```
Print an overview of the network architecture.

## predict

``` python
def predict(self, data, group)
```
Get model predictions for a subset of a Data object. 

 The 'group' argument can have the value 'train', 'val', 'test' or 'all'. The returned array has the shape (number of sequences, number of classes). 



| parameter | type | description |
|:-|:-|:-|
| data | placeholder.Data | A Data object. |
| group | str | The subset of the Data object that should be used for prediction. |

| returns | type | description |
|:-|:-|:-|
| predictions | numpy.ndarray | An array containing predicted probabilities. |
## get\_max\_activations

``` python
def get_max_activations(self, data, group, index = 2)
```
Get the network output of the first convolutional layer. 

 The function returns the maximum activation (the maximum output of a kernel) for every kernel - input sequence pair. The return value is a dict containing the entries 'activations' (an array of shape (number of sequences, number of kernels)), 'labels' (an array of shape (number of sequences, number of classes)) and 'group' (the subset of the Data object used). 

 The 'group' argument can have the value 'train', 'val', 'test' or 'all'. 



| parameter | type | description |
|:-|:-|:-|
| data | placeholder.Data | A Data object. |
| group | str | The subset of the Data object that should be used. |
| index | int | The index of the network layer for which the output should be returned. |

| returns | type | description |
|:-|:-|:-|
| results | dict | A dict with 3 values ('activations', 'labels, 'group', see above) |
## visualize\_kernel

``` python
def visualize_kernel(self, activations, data, kernel, folder)
```
Get a number of visualizations and an importane score for a convolutional kernel. 

 This function creates three output files: 1) a sequence(/structure) motif that the kernel has learned to detect, 2) a histogram/mean activation plot showing the positional enrichment of said motif for every class and 3) violin plots showing the maximum activation  distributions for every class (higher values == better, this is a proxy for general class enrichment). 

 The output files are named "kernel\_x\_motif.png"m "kernel\_x\_position.png" and "kernel\_x\_activations.png" 

 How it works: Given an input sequence, a first layer kernel produces an output vector (called activations) of length sequence\_length - kernel\_length + 1. The position of the maximum activation can therefore be directly mapped back to the input sequence and a subsequence of the length of the kernel can be extracted from the input sequence. Applying this approach to every input sequence yields a number of subsequences that can be used for the construction of a motif. Subsequences are only considered if the maximum activation exceeds a certain threshold, in this case the maximum of the average maximum activations per class. Only subsequences from the top class are used to construct the motif (up to 250 subsequences). 

 The histograms show the positions of the maximum activation, i.e. the positions the subsequences were extracted from. The mean activation plots show the mean activation for all sequence positions. Both plots are only based on sequences that led to a maximum activation higher than the threshold. Histogram and mean activation plot are usually identical, but in case the histogram is very sparse the mean activation plot might be easier to look at. 

 The violin plots show how the maximum activation values are distributed for each class, indicating class enrichment. 

 The function returns a Motif object and an importance score that indicates how important this kernel was for the classification (higher values == more important). The score is computed as maximum of the mean maximum activations per class minus minimum of the mean maximum activations per class. The idea is that kernels that show a big differences across classes (i.e. kernels that are strongly enriched in some classes and little to none in other classes) are more important for the network to deliver correct predictions.abs 



| parameter | type | description |
|:-|:-|:-|
| activations | dict | The return value of the get_max_activations function. |
| data | placeholder.Data | The Data object that was used to compute the maximum activations. |
| kernel | int | The kernel that should be visualized (first kernel is 0) |
| folder | str | A valid folder path. Plots will be saved here. |

| returns | type | description |
|:-|:-|:-|
| (motif, score) | tuple(placeholder.Motif, float) | The motif object and the importance score are returned. |
