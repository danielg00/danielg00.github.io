---
layout: post
title: On the Extrapolative Powers of Neural Networks.
date: 2018-06-03
comments: true
external-url:
categories: AI
---

## Introduction

Extrapolation is an integral part of intelligence.

Vaguely, the two main components of extrapolation are the identification of sub-symbols and the logical synthesis of such sub-symbols into a desired output/label by learning how these sub-symbols interact.
Softmax neural networks seem to pass through this regime in am approximate manner. The main body of a N.N. 'kinda' identifies symbols and classification via softmax function 'kinda' synthesize these 
symbols - albeit, not well and tend to require large amounts of homogeneous data. 

In this blog post I conduct various rudimentary experiments to test the extrapolative abilities of neural networks. The result of the experiments seem to point to towards the composition of softmax NNs lacking
the necessary characteristics to preform rudimentary extrapolation. I emphasize that this obviously isn't justification to abandon deep learning methods, but may point towards us to 
be more careful when deciding the style of output we want. 

Conclusively, neural networks seems specious and only suitable for interpolating. One can think of it as analogous to Monte Carlo methods: it merely estimates using samples from a distribution and 
interpolates between points.

I will speak more on these ideas when we gain more context with the experiments.

___


## Experiments

##### Data

For this experiment I created a two modified version of the MNIST dataset. A single image of the new dataset will consist of two main objects or attributes that make up the image. 

![]({{site.url}}/assets/color_digits_50p.jpg)

This is an image from the first experiement. As you can see it features two main attributes -the color of the digit and the digit itself.

Throughout the rest of the blog post I'll denote the digit as *datum type 1* and the other types as *datum type 2*. Here datum type 2 would be the color of the digits.

![]({{site.url}}/assets/cross_squares_50p.jpg)

This is the data for experiment two. Here datum type 2 is the object at the top left of the image {a cross, a solid box, or exemption of any visible attribute}.

Within each datum there $n$ are sub-datums. For instance, in experiment two, there are $n=3$ sub-datums \(*a cross,a box, absense of a feature*\) making up datum type 2.
These constructions have no real significance and only serve as a means to make what I'm saying more concise and clear.


##### Modus Operandi.

Although the experiment's minutae vary, they all follow the same underlying pattern.

1. We have two types of datum in an image (*e.g colored digits, digit with square at the top left, etc*).
2. We generate a set of pairs, $D_E$ and exclude them from the training process (*e.g red seven, green one etc.*)
3. After training on what is left, $D_T$, we test the network on the excluded pairs.

If a model were to successfully classify these excluded pairs it would mean it would be internally symbolizing each data type and synthesizing these symbols into a label.

##### Encoding.

I use two types of encoding:

__Softmax Encoding:__


To find the index of an image for a one-hot vector we can use the formula

$ i = N_l + M_j  M_n $ 

Here $N_k$, $M_j$ and $M_n$ is the $l^{th}$ datum type 1, the $j^{th}$ datum-type 2 and the total $n$ possible datum types of datum type 1.

__Regressive-like outputs:__

$ O = [M_j, N_k]$

Here I just concatenate labels for the two data types together. An output is correct if each respective entry is within 0.5 of the entries in the label.

This is is perhaps the most basic but preforms badly on even basic classification.

Although completely unusable in real world settings, it makes up what for interpretability  for what it lacks in performance.

##### Model and training.

The network goes as follows:


Conv2d\((f=16,k=[2\times2],s=2\)) $\rightarrow$ BatchNorm1d $\rightarrow$ Maxpool&ReLU\((k=[2\times2\))

$\rightarrow$ Conv2d\((f=32,k=[2\times2],s=1\)) $\rightarrow$ BatchNorm1d $\rightarrow$ Maxpool&ReLU\((k=[2\times2]\)) 

$\rightarrow$ Fully Connected layers dependent on output method.

Where (f), (k), and (s) are the number of convolutions, their kernel size, and their stride, respectively.

I used the same model throughout the experiment. The focus of these experiment was not to achieve state-of-the-art accuracy but to demonstrate extrapolative power, 
therefore the model I defined was quite basic. As you can see in the results below, it has quite paltry performance on MNIST.

I trained the model with RMSprop for 1500 iterations with a learning rate of 0.001 and batch size of 128.

Little of this matters, I'm just trying to fill what would have been an empty column with text.
 
 
Experiment #1.  #Note to self, Should touch on consequences on R.L .

The first experiment I conducted was on a colored version of MNIST.

Colored MNSIT digits

Here the two categories are color (red, green, blue) and digit (0, ..., 9).

The network preforms well on the original task but preforms poorly (0% accuracy) when it comes to extrapolation.

exper1

Where A, B, C are the accuracy on the trained data, the accuracy on the the excluded data, and the decrease of accuracy between the two respectively.

I will comment on all the results later.
Experiment #2.

The second is an experiment more apt for convolutions. Instead of having to realize colors the model must simply recognize either solid square in the top left. As you can see, we've also reverted back to the black and white, 1 channel images.

crosses_squares
	##results##

___

## Discussion.
Regressive output.

As stated, the regressive outputs provide little real-world utility but yield interesting heuristic information. For instance, in experiment #1 it succeeds in classifying the digit correctly but fails in recognizing it's color.

In experiment #2 we observe the the converse. The model does worse when recognizing digits but classifies the second data type in the image better. Digits are ~5% better than random choice, and shapes ~ 27% better that random choice.
Softmax output.

As you might of realized, softmax does worse than randomly guessing. Not only this, but it as training progresses its accuracy become worse. This could be analogous to the concept of over-fitting. As the network fits for more data in input space it does this as the expense of certain other sectors in the form of assigning it to certain labels.

Ultimately, it is clear that
Visualization.

Using [PCA](https://plot.ly/~danielg00/6.embed) we can see the input space being laid out as expected. There are three stratifications accounting for the variability of the data containing a box/cross/or nothing and ten amorphous stratifications orthogonal to the three.
Conclusion.

Given the nature of the input space, it seems that the softmax function and using logits makes neural networks ill-equipped to deal with. It will only ever fit data onto what it sees, and
Need to expand on ... Plot embeddings of output of trained network

TODO:
    Create table of results
    Links to reasoning.
    Whats needed to implement this.
    Transfer learning.
    Reinforcement learning.
    Geometric explanation of what happening.
    Could compare spaces of model trained with no exclusion and model.

<!--  LocalWords:  dataset
 -->
