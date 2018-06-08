---
layout: post
title: What it means for a concept to be logically labelled
date: 2018-06-03
comments: true
external-url:
categories: AI
---

## Introduction
In this post I exposit on what it means for a concept or piece of data to be logicaly labelled. For context on how we present data in this section I'd advise you to read [this](Extrapolative-Powers-of-Neural-Networks.html) other blog post. 

We ca synthesis our own data to aid understanding. This data is analogous but can be plotted in 3-d space. It consists of an array of 3 cells {A, B, C}; each having the choice to be on or off. Our goal then, is to classify each possible state in our array, therefore the output
Feature entailments and other things...

\leftrightarrow

\rightarrow


What is required of an algorithm is to realize how certain features (i.e. the two datum types in the image) interact with each-other to give rise to a new set of features (In this example, one hot encoding has insufficient information, but we can still map it to a regular vector where a algorithm then maps this to a one-hot output). To further understand logical entailment of features we must introduce some formalization.

We will say that two features $latex X, Y $ interact with each other, $latex X \leftrightarrow Y $, and will entail, $latex \rightarrow $, another set of features.

We observe that a feature $latex X $ interacting with nothing, $latex \cdot $, will always entail the same feature $latex  x $.

$latex (X \leftrightarrow \cdot) \rightarrow x $

Perhaps the most simple, inoffensive entailment has distributive properties.

$latex ((X \leftrightarrow \cdot) \leftrightarrow (Y \leftrightarrow \cdot)) \rightarrow xy $

There obviously exists more intricate interaction. For instance maybe a feature triggers something when it interacts with a specific type of feature. This will lead to non-simplistic entailments.

We can obviously frame solving our mock dataset using this idea but also anything that contains features of some sort that logically entail something (a label, a new environment etc). But for now we'll keep focus on our mock dataset.

Real world examples

I'll use the data form experiment #2 for illustration. We'll denote datum type 1 & 2 as $latex D_1 \ \& \ D_2 $ . $latex D_1 $ could be an X, a black box or completely absent. $latex D_2 $ could be and MNSIT digit from 0 to 9.

We make the simplifying assumption here that $latex D_1 \ \& \ D_2 $ are the same feature. In reality, I'd imagine we'd need to individually assign the notion of a feature to each type of datum in $latex D_1 \& D_2 $. We also assume and know that the interaction taking place are of the simple type.

if   $latex (D_n\leftrightarrow \cdot) \rightarrow d_n $

then $latex ((D_1 \leftrightarrow \cdot) \leftrightarrow (D_2 \leftrightarrow \cdot)) \rightarrow d_1 d_2 $

Often, we cannot generate examples as we like and are restricted to our dataset. This presents the problem of distilling what features. This can crudely solved using something analogous to slow feature analysis. Assuming simple interaction, we can find isolate feature entailments using a series arithmetic operations.

For instance:

if   $latex (X \leftrightarrow Y) \rightarrow Z_1 $

and $latex (X \leftrightarrow \beta) \rightarrow Z_2 $

then it stands that feature entailment of X would be the 'slow feature'/persistent feature between $latex Z_1 \ \& \ Z_2 $


How can these rules be applied? Obvious application lie in typical classification problems and reinforcement learning of environments. The notion here are related to transfer learning.

We can use this concept in typical classification with macro-features and micro-features: macro-features being an 'X' or digit, micro-features being a straight lines, curves etc. It is important to include a sense of spatial co-ordinate or relative position in these feature.

Learning under this regime would also make whatever model learn what a label/object is relative to other objects. Perhaps is will realize that the digit '7' is similar to a '1' but with a straight line on top of it.

These ideas are applicable to reinforcement learning, but often would require non-simplistic interaction.

