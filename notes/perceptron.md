---
title: perceptron
date: 2017-06-06 07:00:00
tags:
  - deep learning
  - machine learning
  - data mining
categories: notes
---

# lecture 2a
## an overview of the main types of neural network architecture

* feed-forward neural networks(more than one hidden layer call them "deep" neural networks)
* recurrent networks
these have directly cycles in their connection
- for modeling sequences
* symmetrically connected networks


# lecture 2b

## statistical pattern recognition
1. convert the raw input vector into a vector of feature activations
2. learn how to weight each of the feature activations to get a single scalar quantity
3. if this quantity is above some threshold decide that the input vector is positive example of the target class
## architecture 
decision unit
learned weights
feature units
hand-coded weights or programs
input units
## history 
* 1960's 
* 1969 minsky shows perceptrons limits, and many people thought theses limitations applied to all neural network models.
* the perceptrons is still widely used today for tasks with enormous feature vectors that contain many millions of feature
## binary threshold neuron(decision unit)
* mcculloch-pitts(1943)
$$
z = \sum_{k=1}^n xw +b
$$
y = 1 if z >= 0 else 0
## how to biases using the same rule  as we use for learning weights
* A threshold  is equivalent to having a negative bias
* We can avoid having to figure out a separate learning rule for the bias by using a trick:
- A bias is exactly equivalent to a weight on an extra input line that always has an activity of 1
- we can now learn a bias as if it were a weight

## the perceptron convergence(important!) :procedure training  binary out neuron as classifiers

* add an extra component with value 1 to each input vectors . The "bias" weight on this component is minus the threshold.Now we can forget 
* pick training cases using any policy that ensures that every  training case will keep getting picked
* the procedure:
- if the output unit is correct, leave its weight alone
- if the output unit in correctly output a zero, add the input vector to the weight vector
- if the output unit incorrectly output a 1, subtract the input vector
from the weight vector
* this is guaranteed to find a set of weights that gets the right answer for all the training cases  if any such set exists

# lecture 2c
# geometrical view of perceptrons


## weights space

* this space has one dimension  per wights
* a point in the space represents a particular setting of all the weights
* assuming that we have eliminated the threshold, each training case can be represented as a hyperplane through the origin 
- the weights must lie on one side of this hyper-plane to get the answer correct
* each training case defines a plane 
- on one side of the plane the output is wrong because the scalar product of the weight vector with the input vector has the wrong sign.
## the cone(圆锥) of feasible solutions
* to get all training case right we need to find a point on the right side of all the planes
* if there are any weight vector that get the right answer for all cases, they lie in a hyper-cone with its apex at the origin .
- the average of two good weight vector is a good vector 
* so the problem is convex
 
# lecture 2d
## why the learning works
* consider the squared distance $$ d^{2}_{a} + d^{2}_{b} $$between any feasible weight vector and the current weight vector
- hopeful claim: every time the perceptron make a mistake, the learning algorithms moves the current weight vector closer to all feasible weight  vectors.
## informal sketch of proof of convergence
* each time the perceptron makes a mistake ,the current weight vector  moves to decrease its squared distance from every weight vector in the "generously feasible" region.
* the squared distance decrease by at least the squared length of the input vector
* so after a finite number of mistake, the weight vector must lie in the feasible region if this region exists

# lecture 2e
# what perceptron can't do

## the limitations of perceptrons

* if you are allowed to choose the features by hand and if you use enough features ,you can do almost anythings
- for binary input vectors, we can have a separate feature use each of the exponentially many binary vectors and so we can make any possible discrimination on binary input vectors.
* this type of table look-up won't generalize
* but once the hand-coded feature have been determined, the are very strong limitations on what a perceptron can learn 

## what binary threshold neuron cannot do 
* a binary threshold output unit cannot even tell if two single bit feature are the same
positive case (same): (1,1)->1,(0,0)->1
negative case (different): (1,0)->0,(0,1)->0

* the four input-output pairs give four inequalities to satisfy:

$$ w_{1}+w_{2} >= \theta ,0 >= \theta $$
$$ w_{1} < \theta , w_{2}< \theta $$
## geometric view of what binary threshold neuron cannot do
* imagine "data-space" in which the correspond to component of an input vector
- each input vector is a point in this space
- a weight vector defines a plane in data-space
- the weight plane is perpendicular to the weight vector and misses the origin by a distance equal to the threshold 
- not linearly separate
##  discriminating simple patterns under translation with wrap-around
* suppose we just use pixels as the features.
* can a binary threshold unit discriminate between different patterns that have the same number of on pixels
- not if the patterns can translate with wrap-around
## sketch of a proof that a binary decision unit cannot discriminate patterns with the same number of on pixels(assuming translation with wrap-around)
* for pattern A, use training cases in all possible translations.
- each pixels will be activated by 4 different translations of pattern A
- so the total input received by the decision unit over  all these patterns will be four times the sum of all the weight

* for pattern B, use training cases in all possible translations.
- each pixels will be activated by 4 different translations of pattern B
- so the total input received by the decision unit over  all these patterns will be four times the sum of all the weight

* but to discriminate correctly ,every single case of pattern A must provide more input to decision unit than every case of pattern B
- this is impossible if the sums over cases are the same

## why this result is devastating for perceptrons
* the whole point of pattern recognition is to recognize pattern despite transformations like translation
* minsky and papert's "Group invariance theorem" says that the part a perceptron that learns cannot learn to do this if transformations form a group
- translation with wrap-around form a group
 
* to deal with such transformations ,a perceptron needs to use multiple feature unit to recognize transformations of informative sub-patterns
- so the tricky part of pattern recognition must  be solved  by the hand-coded
feature detector, not the learning  procedure.
## learning with hidden units 
* networks without hidden units are very limited in the input-output mappings the can learn to model.
- more layers of linear units do not help, its still linear
- fixed output no-linearities are not enough
* we need multiple layers of adaptive, no-linear hidden units . but how can we train such nets?
- we need an efficient way of adapting all the weight  ,not just the last layer
- learning  the weights going into hidden units is equivalent to learning features
- this is difficult because nobody is telling us directly what the hidden units should do
* the hidden units became the features detector !

