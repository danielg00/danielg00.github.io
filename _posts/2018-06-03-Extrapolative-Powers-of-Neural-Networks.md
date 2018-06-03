---
layout: post
title: On the Extrapolative Powers of Neural Networks.
date: 2018-06-03
comments: true
external-url:
categories: AI
---


## Introduction

(*I'll upload and link the code in Github once I clean it up. It might take a while though.*)


Extrapolation is a vital part of getting machines to exhibit intelligence. Extrapolation is one of the under-lying mechanisms of general intelligence.

In this blog post I conduct various rudimentary experiments to test the extrapolative abilities of neural networks. I turns out that perhaps typical models do not have the necessary a priori knowledge to logically infer about data. This a priori knowledge is that from certain features arise others features. It is a model's goal to recognize this and synthesis these sequences of features given past knowledge.

In this sense, neural networks seems specious and only fit for interpolating. One can think of it as analogous to Monte Carlo methods: it merely estimates using samples from a distribution and interpolates between points. Ultimately this seems unfeasible unless we can sample from some aseptic distribution of pure logic.

Drawing form a physical analogy; if one we trying to derive the shape of bowl, neural networks rain water on it and where each drop collides with something. Humans on the other hand would innovate a shape that matches the criteria of what bowl does.
> SPEAK HERE ABOUT GOAL OF ELUCIADATING FEATURE SYNTHESIS WITH CREATED DATASETS 

## Experiments
##### Data
For this experiment I created a two modified version of the MNIST dataset. A single instance of the new dataset consist of two main objects/attributes that make up the image. 


![]({{site.url}}/assets/color_digits_50p.jpg)


This is the modfied dataset for the first experiement. As you can see it features two mains datums-the color of the digit and the digit itself.

Throughout the rest of the blog post I'll denote the feature of digits as *datum type 1* and the other datum as *datum type 2*. Here datum type 2 is the color of the digits.


![]({{site.url}}/assets/cross_squares_50p.jpg)


This is the dataset for experiement two. Here datum type 2 is the object at the top left of the image. 

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

###### Softmax Encoding:

To encode the two type of datum into one one-hot vector we can use the formula $N_i + M_i  M_n $ to find its index.
Here $N_i$, $M_j$ and $M_n$ is the $i^{th}$ datum of one type, the $j^{th}$ of the other and the total $n$ possible datum types of datum A



Regressive outputs:

$ O = [M, N]$

Here I just concatenate labels for the two data types together. An output is correct if each respective entry is within 0.5 of the entries in the label.

This is is perhaps the most basic but preforms badly on even basic classification.

Although completely unusable in real world settings, it makes up what for interpretability  for what it lacks in performance.

Model and training.

The network goes as follows:


Conv2d\((f=16,k=[2\times2],s=2\)) $\rightarrow$ BatchNorm1d $\rightarrow$ Maxpool&ReLU\((k=[2\times2\))

$\rightarrow$ Conv2d\((f=32,k=[2\times2],s=1\)) $\rightarrow$ BatchNorm1d $\rightarrow$ Maxpool&ReLU\((k=[2\times2]\)) 

$\rightarrow$ Fully Connected layers dependant on output method.

Where (f), (k), and (s) are the number of convolutions, their kernel size, and their stride.

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
 
3. Analysis.
Regressive output.

As stated, the regressive outputs provide little real-world utility but yield interesting heuristic information. For instance, in experiment #1 it succeeds in classifying the digit correctly but fails in recognizing it's color.

In experiment #2 we observe the the converse. The model does worse when recognizing digits but classifies the second data type in the image better. Digits are ~5% better than random choice, and shapes ~ 27% better that random choice.
Softmax output.

As you might of realized, softmax does worse than randomly guessing. Not only this, but it as training progresses its accuracy become worse. This could be analogous to the concept of over-fitting. As the network fits for more data in input space it does this as the expense of certain other sectors in the form of assigning it to certain labels.

Ultimately, it is clear that
Visualization.

Using PCA we can see the input space being laid out as expected. There are three stratifications accounting for the variability of the data containing a box/cross/or nothing and ten amorphous stratifications orthogonal to the three.
Conclusion.

Given the nature of the input space, it seems that the softmax function and using logits makes neural networks ill-equipped to deal with. It will only ever fit data onto what it sees, and
Need to expand on ... Plot embeddings of output of trained network

    links to reasoning.
    whats needed to implement this.
    transfer learning.
    reinforcement learning.
    geometric explanation of what happening.
    Could compare spaces of model trained with no exclusion and model

