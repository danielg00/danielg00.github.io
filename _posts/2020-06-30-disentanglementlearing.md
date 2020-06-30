---
layout: post
title: A quick catch-up in Disentanglement Learning.
date: 2020-06-30
comments: true
external-url:
categories: AI
---

### Preamble
Disentanglement learning aims to learning features or representations that are independent of their embedded context. A concrete example of where disentanglement learning becomes useful is for basic 
extrapolation tasks. For instance, show an observer a scene of a basketball on a wall and give it a label. Then show it a bottle on its own or in some other context and give it another label. If we've learned 
a disentangled representation of these two inputs, the observer should be able to deduce the label for a scene with a bottle on a wall. It sounds painstakingly simple, but nonetheless an example of emergent extrapolation, in a sense. Arguably it forms the basis for simple extrapolation.

[[1]](https://arxiv.org/abs/1301.3781) does something similar in their paper on Word2Vec, demonstrating how the embedding space can [model analogies](https://towardsdatascience.com/how-to-solve-analogies-with-word2vec-6ebaf2354009?gi=5419100a6e07). For instance, if one wished to solve the analogy "Man is to Woman, as King is to ?(Queen)". One can 
get the word vectors $v_{man}, v_{woman}, v_{king}$, and see that $v_{king} - v_{man} + v_{woman} \approx v_{queen}$. Assuming that each word has some feature such as "royalty" and "gender", one can see
how this is an "analogy" for disentanglement learning.

The explanation of the task given [here](https://deepai.org/machine-learning-glossary-and-terms/disentangled-representation-learning) on deepai.org feels vague:

*Disentangled representation is an unsupervised learning technique that breaks down, or disentangles, each feature into narrowly defined variables and encodes them as separate dimensions. 	The goal is to mimic the quick intuition process of a human, using both “high” and “low” dimension reasoning. For example, in a predictive network processing images of people, “higher dimensional”
features such as height and clothing would be used to determine sex. In a generative network version of that model designed to produce images of people from a stock photo database, these would be 
broken down into separate, lower dimensional features. Such as: total height of each person, length of arms and legs, type of shirt, type of pants, type of shoe, etc…*

Indeed, we see that perhaps the notion of disentanglement learning is ill-posed in the unsupervised setting; perhaps it's not the notion of learning disjoint representations that is needed but the notion
of discovering what features deterministically induce labels/outputs. This seems like prime territory for [GNNs](https://arxiv.org/abs/1812.08434) and I'll be writing more on it at a later date.


### Current Research
The current research around disentanglement learning seems underwhelming, and the few theoretical results don't yield promising conclusions! [[2]](https://arxiv.org/abs/1811.12359) shows that many of the models
tailored towards disentangled learning in unsupervised settings are deficient
	
*We first theoretically show that the unsupervised learning of disentangled representations is fundamentally impossible without inductive biases on both the models and the data. [...] 
	Then, we train more than 12000 models covering most prominent methods and evaluation metrics in a reproducible large-scale experimental study on seven different data sets. 
We observe that while the different methods successfully enforce properties "encouraged" by the corresponding losses, well-disentangled models seemingly cannot be identified without supervision.*

[[3]](https://papers.nips.cc/paper/7333-learning-to-decompose-and-disentangle-representations-for-video-prediction.pdf) is a nice paper where the "label" for a video frame can be interpreted as the subsequent
video frame in the task of predicting videos by disentangling video frames.

An obvious(if not the biggest) problem is that disentanglement learning must implicitly solve the problem of recognizing objects under transformations (i.e. rotations, translations, etc.). 
Deepmind's paper [[4]](https://deepmind.com/research/publications/towards-definition-disentangled-representations) attempts to define the task under this scheme. To quote: 

*Here we propose that a principled solution to characterising disentangled representations can be found by focusing on the transformation properties of the world.* 

They propose that a group $G$ acts on a space $X$ through $\cdot:G \times X \rightarrow X$, and that $G$ decomposes into the product of subgroups $G = G_1 \times G_2 \times ... $. Perhaps one interesting 
generalisation of this idea is that $G$ acts on the powerset $\mathcal{P}(X)$. That is, the map may not be bijective and that certain features "collapse". One could leverage this to explain (or
devise) algorithms in the supervised setting - particularly maps to one-hot labels.

To be continued...

	
	



