---
title: "Neural Network from scratch"
permalink: /nn-from-scratch/
date: 2020-10-17
layout: splash
comments: true 
author_profile: true
related: true
share: true
read_time: true
tags:
    - blog

header:
  image: "/assets/images/blog-head-neural-network_16-August-2020.jpg"
  teaser: "/assets/images/KM_blog-teaser-banner-1_16-August-2020.jpg"
excerpt: "Neural Network, Deep Learning"
mathjax: "true"
toc: true

---

Humans have been fairly obsessed with the idea of a machine doing things for them, or at least make their life easier for them, for a very long time now. Starting right from the invention of Wheel to the invention of Computer we pushed the limits of our brain to build such amazing objects. But something changed at the invention of computer, we realised that computers are far too good in one particular aspect as compared to humans, Calculations!
Then the human obsession of beating the computers at their own game began. We had some truly great human minds who not only challenged but won against the computer, may it be Shakuntala Devi beating the computer in finding the 23rd root of a 50 digit number or Garry Kasparov beating IBM's Deep Blue in chess matches. But soon we came to realise that computers(given correct configurations) are truly unbeatable at all the things that we previously won. So our focus shifted towards making use of the computers' calculative capabilities to solve problems which we find difficult. 

While this was happening though, some scientists were working on generating a mathematical model that would "learn". The inspiration of that coming from the most perfect object that we knew which already learnt and developed was a Brain. Thus combining the power of huge calculations and the mathecatical modela that could learn, the idea of a Neural Network(Multilayered Perceptron) was born.


## What is a Neural Network?
**Neural Networks** are basically an attempt to make a mathematical model of the brain. Let's see the working of a single neuron, 

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/biological_neuron.png" alt="biological neuron"> 



But even though idea of a biological neuron being an inspiration is pretty interesting, I find it much easier to see a neuron as mathematical function that maps given input with a desired output:

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/artificial_neuron.png" alt="artificial neuron"> 

As you can see the input values $$x_1$$, $$x_2$$, $$x_3$$, multiplied by some weights, are passed into some function $$\sigma$$ and value of output is $$y = \sigma(x_1 \times w_1 + x_2 \times w_2 + x_3 \times w_3)$$. But I must admit here that I have grossly oversimplified this whole process of neural network flow and even though the basic idea remains the same, there are multiple components and steps involved in the working of a neural network.

So without further adieu let us dive into the basics of Neural Network Architecture.


## Architecture of a Neural Network
Let's start small, as we saw in the above diagram, there's an "input layer", a "function layer" and a "output layer", with funtion layer and output layer containing only single neuron. If we were to extrapolate this idea and increase the number of neurons in each layer and the number of hidden layers, the architecture would look something like this:

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/NN_architecture.png" alt="Neural Network architecture"> 



## Components of a Neural Network flow

To save myself from the confusion I divided the whole process of a neural network training into 5 parts:
* Input Matrix
* Weights, Bias and Activation funtions
* Feedforward process
* Loss Calculation
* Updating the weights

### Input Matrix

The main idea of a neaural network is to be able to solve our problems.

# H1 Heading

## H2 Heading

### H3 Heading

Here's some basic text

And here's some in *italics*

Here's some **bold**

What about a [link](https://github.com/aknottymathematician)?

Here's a bulleted list:
* First item
+ Second item
-Third item

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
    import numpy as np
    
    def test_function(x,y):
      z = np.sum(x,y)
      return z
```
Here's some inline code `x+y`

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/youtube-recommender-system.png" alt="youtube recommender system">

Here's another image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/youtube-recommender-system.png)

Here's some math:

$$z=x+y$$

You can also put it inline $$z=x+y$$
