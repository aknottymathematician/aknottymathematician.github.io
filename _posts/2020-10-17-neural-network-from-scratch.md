---
title: "Neural Network from scratch"
permalink: /nn-from-scratch/
date: 2020-10-17
layout: single
classes: wide
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

mathjax: "true"
toc: true

---

Humans have been obsessed with the idea of a machine doing things for them, or at least make their life easier for them, for a very long time now. Starting right from the invention of Wheel to the invention of Computer we pushed the limits of our brain to build such amazing objects. But something changed at the invention of computer, we realised that computers are far too good in one particular aspect as compared to humans, Calculations!

Then the human obsession of beating the computers at their own game began. We had some truly great human minds who not only challenged but won against the computer, may it be Shakuntala Devi beating the computer in finding the 23rd root of a 50 digit number or GM Garry Kasparov beating IBM's Deep Blue in chess match. But soon we came to realise that computers(given correct configurations) are truly unbeatable at all the things that we previously won against them. So our focus shifted towards making use of the computers' calculative capabilities to solve problems which we found difficult. 

While this was happening though, some scientists were working on generating a mathematical model that would "learn". The inspiration of that coming from the most perfect object that we knew, which already learnt and developed was, a Brain. Thus combining the power of huge calculations and the mathematical models that could learn, the idea of a Neural Network(Multi Layered Perceptron) was born.






## What is a Neural Network?
**Neural Networks** are basically an attempt to make a mathematical model of the brain. 

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/biological_neuron.png" alt="biological neuron"> 

A Bio 

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/artificial_neuron.png" alt="artificial neuron"> 

You can see the similarities between the biological artifial structures. The idea of a biological neuron being an inspiration is pretty interesting, but I find it much easier to see a neuron as mathematical function that maps given input with a desired output:

Let's see the working of a single neuron, the input values $$x_1$$, $$x_2$$, $$x_3$$, multiplied by some weights, are passed into some function $$\sigma$$ and value of output is $$y = \sigma(x_1 \times w_1 + x_2 \times w_2 + x_3 \times w_3)$$. We call this "single layered" structure a Perceptron. But I must admit here that I have grossly oversimplified this whole process of neural network flow and even though the basic idea remains the same, there are multiple components and steps involved in the working of a neural network.

So without further adieu let us dive into the basics of Neural Network Architecture.


## Architecture of a Neural Network
Let's start small, as we saw in the above diagram, there's an "input layer", a "function layer" and a "output layer", with funtion layer and output layer containing only single neuron. This structure is called a perceptron. If we were to extrapolate this idea and increase the number of neurons in each layer and the number of "function" layers we get a MLP(Multi Layered Perceptron), the structure would look something like this:

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/NN_architecture.png" alt="Neural Network architecture"> 

In the above architecture, there are four layers - 
* 1 Input Layer with 3 neurons
* 2 Hidden(Function) Layers with 4 neurons each
* 1 Output Layer with 2 neurons
  

### Components in architecture of a Neural Network 
**Neuron -** A neuron is the most basic unit of a Neural Network. Each neuron stores information either as a real number or a mathematical operation that takes input, multiplies it by it's weights and then passes the sum through the activation function to the other neurons.

**Layer -** A layer is multiple neurons working together. Input Layer takes in the data in form of vectors. Hidden layer processes that data using functions which we call activation functions. Output layer gives us the final result after the data has passed through the whole architecture.

Theoretically there is no restriction on the number of neurons in each layer or the number of layers, but in practice there is an upper limit to these numbers. What is this limit depends on the processing power of the system, latency limit and of course the cost of the financial cost of the system that would perform such calculations.

[TOP](#){: .btn .btn--danger}

### Workflow of a neural network

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/flow_of_nn.png" alt="Flow of NN"> 



## Components of a Neural Network flow

To save myself from the confusion I divided the whole process of a neural network training into 5 parts:
* Input Matrix
* Weights, Bias and Activation functions
* Feedforward process
* Loss Calculation
* Backpropagation

### Input Matrix

The main idea of a neural network is to be able to solve our problems and there is no shortage of the problems that can be solved, may it be classification or regression or unsupervised learning. But here's where it gets a little tricky, all the operations that we do are mathematical in nature and we won't always get the data which is numerical, for example text data, what do we do in that case?

Well, let's take a simple example we have to classify fruits with features as colour, taste, mass and two types of fruits(classes) Apple and Orange. Now mass is a numerical value, shouldn't be a problem when it passes through the NN. However colour and taste are text values, but there is a simple way out here, since meanings of the words red and orange are not required but only the value that they posses we can simply index them({"red":0, "orange":1}) and use those numbers as inputs for NN. Same goes for the feature taste. 

However things don't remain that simple when meanings of the words matter, example say we are building a model which will classify the given sentence as positive or negative. In that case, simply assigning a number to each word won't help since the number of unique words can be in millions!

I will be covering the concepts of NLP and how we would solve this problem, in depth, in future blogs. For now it is enough to know that we vectorize the words or sentences and number of neurons in input layer is same as the dimension of the word or sentence vectors.

Basically an input for NN with $$n$$ input neurons is a matrix of dimension $$n \times 1$$.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/input_matrix.png" alt="input matrix"> 


### Weights, Bias and Activation functions




### Feedforward process
Forward propagation is a process of feeding input values to the neural network and getting an output which we call predicted value. When we feed the input values to the neural network’s first layer, it goes without any operations. Second layer takes values from first layer and applies multiplication, addition and activation operations and passes this value to the next layer. Same process repeats for subsequent layers and finally we get an output value from the last layer.



### Loss Calculation




### Backpropagation







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
