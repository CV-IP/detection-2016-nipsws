# Hierarchical Object Detection with Deep Reinforcement Learning

|  ![NIPS 2016 logo][logo-nips] | Paper accepted at [Deep Reinforcement Learning Workshop, NIPS 2016](https://sites.google.com/site/deeprlnips2016/)   |
|:-:|---|

[logo-nips]: http://hci-kdd.org/wordpress/wp-content/uploads/2014/11/Neural-Information-Processing-2016.jpg "NIPS 2016 logo"

| ![Míriam Bellver][bellver-photo]  | ![Xavier Giro-i-Nieto][giro-photo]  | ![Ferran Marqués][marques-photo]  | ![Jordi Torres][torres-photo]  |
|:-:|:-:|:-:|:-:|:-:|
| [Míriam Bellver][bellver-web]  | [Xavier Giro-i-Nieto][giro-web]  |  [Ferran Marques][marques-web] | [Jordi Torres][torres-web]  |


[bellver-web]: https://www.bsc.es/bellver-bueno-miriam
[giro-web]: https://imatge.upc.edu/web/people/xavier-giro
[torres-web]: http://www.jorditorres.org/
[marques-web]:https://imatge.upc.edu/web/people/ferran-marques

[bellver-photo]:  https://github.com/imatge-upc/detection-2016-nipsws/blob/master/authors/MiriamBellver160x160.jpg?raw=true "Míriam Bellver"
[giro-photo]: https://github.com/imatge-upc/detection-2016-nipsws/blob/master/authors/XavierGiro160x160.jpg?raw=true "Xavier Giro-i-Nieto"
[marques-photo]: https://github.com/imatge-upc/detection-2016-nipsws/blob/master/authors/FerranMarques160x160.jpg?raw=true "Ferran Marques"
[torres-photo]:  https://github.com/imatge-upc/detection-2016-nipsws/blob/master/authors/JordiTorres.jpg?raw=true  "Jordi Torres"

A joint collaboration between:

|![logo-bsc] | ![logo-gpi]  |
|:-:|:-:|:-:|
| [Barcelona Supercomputing Center][bsc-web] | [UPC Image Processing Group][gpi-web] |

[gpi-web]: https://imatge.upc.edu/web/ 
[bsc-web]: http://www.bsc.es 

[logo-bsc]:https://github.com/imatge-upc/detection-2016-nipsws/blob/master/logos/bsc320x86.jpg?raw=true "Barcelona Supercomputing Center"
[logo-gpi]: https://github.com/imatge-upc/detection-2016-nipsws/blob/master/logos/gpi320x70.png?raw=true "UPC Image Processing Group"

## Publication
### Abstract

 We present a method for performing hierarchical object detection in images guided by a deep reinforcement learning agent. The key idea is to focus on those parts of the image that contain richer information and zoom on them. We train an intelligent agent that, given an image window, is capable of deciding where to focus the attention among five different predefined region candidates (smaller windows). This procedure is iterated providing a hierarchical image analysis.
 
We compare two different candidate proposal strategies to guide the object search: with and without overlap. Moreover, our work compares two different strategies to extract features from a convolutional neural network for each region proposal: a first one that computes new feature maps for each region proposal, and a second one that computes the feature maps for the whole image to later generate crops for each region proposal. 

Experiments indicate better results for the overlapping candidate proposal strategy and a loss of performance for the cropped image features due to the loss of spatial resolution. We argue that, while this loss seems unavoidable when working with large amounts of object candidates, the much more reduced amount of region proposals generated by our reinforcement learning agent allows considering to extract features for each location without sharing convolutional computation among regions.


## Code Instructions

This python code enables to both train and test each of the two models proposed in the paper. The image zooms model extracts features for each region visited, whereas the pool45 crops model extracts features just once and then ROI-pools features for each subregion. In this section we are going to describe how to use the code.

### Setup

First of all the weights of VGG-16 should be downloaded from the following link [VGG-16 weights]. If you want to use some pre-trained models for the Deep Q-network, they can be downloaded in the following links [Image Zooms model] and [Pool45 Crops model].You should also create two folders in the root of the project, called models_image_zooms and models_pool45_crops, and store inside them the corresponding weights. 


[VGG-16 weights]: https://drive.google.com/file/d/0Bz7KyqmuGsilT0J5dmRCM0ROVHc/view?usp=sharing
[Image Zooms model]: 
[Pool45 Crops model]:


### Usage

##### Training

We will follow as example how to train the Image Zooms model, that is the one that achieves better results. The instructions are equal for training the Pool45 Crops model. The script is image_zooms_training.py, and first the path to the database should be configured:

PATHS

The enables checkpointing, so you should indicate which epoch you are going to train. If you are training it from scratch, then the training command should be:

python image_zooms_training.py -n 0

There are many options that can be changed to test different configurations:

Number of steps: For how many steps you want your agent to search for an object in an image.

Subregion scale: The scale of the subregions in the hierarchy, compared to its ancestor. Default value is 3/4, that denoted good results in our experiments, but it can easily be set. Take into consideration that the subregion scale and the number of steps is very correlated, if the subregion scale is high, then you will probably require more steps to find objects.

Drawing: 


##### Testing

In this case, you should use the script image_zooms_testing.py. You should also configure the paths to indicate which weights you want to use. In this case, you should only run the command python image_zooms_testing.py. It is recommended that for testing you put bool_draw = 1, so you can observe the visualizations of the object search sequences. 






