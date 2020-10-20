---
title: "An ever expanding collection of ML & DL terminologies"
layout: single
classes: wide
toc: true
permalink: /glossary/
author_profile: true
taxonomy: glossary
entries_layout: list
mathjax: true
header:
  image: "/assets/images/KM_glossary_19-October-2020.png"
  
---

## Activation Functions

### Step Function

Equation for Step Function
$$  f(x) =
\begin{cases}
0,  & x \lt 0 \\
1, & x \geq 0 
\end{cases}$$

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/step_function.png" alt="step function">


### ReLU

Equation for Rectified Linear Unit(ReLU) activation function
$$  f(x) =
\begin{cases}
0,  & x \lt 0 \\
x, & x \geq 0 
\end{cases}$$

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/ReLU.png" alt="ReLU">


### Sigmoid

Equation for Sigmoid
$$ f(x) =  \frac{\mathrm{1} }{\mathrm{1} + e^-x }  $$ 
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sigmoid.png" alt="Sigmoid">

### Tanh

### Leaky ReLU


## Components of NN

### Activation Function

### Bias

Bias is a non-zero number defined by us and it acts the same way as $$c$$ does in the equation $$y = m\times x + c$$.

### Neurons

A neuron is the most basic unit of a Neural Network. Each neuron stores information either as a real number or a mathematical operation that takes input, multiplies it by it's weights and then passes the sum through the activation function to the other neurons.


### Weights

Weights decide the importance of the input coming into a neuron. Weights are initialised randomly in the beginning, later however they are automatically calculated based on the output.

## Loss Functions

### MSE(Mean Squared Error)

### RMSE(Root Mean Squared Error)

### Log Loss