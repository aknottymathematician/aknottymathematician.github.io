---
title: "An ever expanding collection of ML & DL terminologies"
layout: single
classes: wide
permalink: /glossary/
author_profile: true
taxonomy: glossary
entries_layout: list
mathjax: true
header:
  image: "/assets/images/KM_glossary_19-October-2020.png"
  
---


<!-- <details>
<summary>1. Activation Functions </summary>
<br>
[ReLU](#relu)
<br>
[Sigmoid](#sigmoid)
<br>
[Tanh](#tanh)
<br>
</details> -->
## <ins>Table of Content</ins>

<details>
<summary>
<i>Activation Functions </i>
</summary>
<a href="https://aknottymathematician.github.io/glossary/#step-function">
Step Function</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#relu">
ReLU</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#sigmoid">
Sigmoid</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#tanh">
Tanh</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#leaky-relu">
Leaky ReLU</a>
<br>
</details>

<details>
<summary>
<i>Components of NN </i>
</summary>
<a href="https://aknottymathematician.github.io/glossary/#activation-function">
Activation Function</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#bias">
Bias</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#neuron">
Neuron</a>
<br>
<a href="https://aknottymathematician.github.io/glossary/#weights">
Weights</a>
<br>
</details>
<!-- 1. [Example](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)
4. [Fourth Example](#fourth-examplehttpwwwfourthexamplecom)


## Example
## Example2
## Third Example
## [Fourth Example](http://www.fourthexample.com)  -->

### Activation Functions

#### Step Function

Equation for Step Function
$$ f(x) =
\begin{cases}
0,  & x \lt 0 \\
1, & x \geq 0 
\end{cases} $$
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/step_function.png" alt="step function">


#### ReLU

Equation for Rectified Linear Unit(ReLU) activation function
$$  f(x) =
\begin{cases}
0,  & x \lt 0 \\
x, & x \geq 0 
\end{cases} $$
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/ReLU.png" alt="ReLU">


#### Sigmoid

Equation for Sigmoid
$$ f(x) =  \frac{\mathrm{1} }{\mathrm{1} + e^{-x} }  $$ 
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sigmoid.png" alt="Sigmoid">

#### Tanh

Equation for Tanh
$$ f(x) =  \frac{e^{x} - e^{-x} }{e^{x} + e^{-x} }  $$ 


#### Leaky ReLU

Equation for Rectified Linear Unit(ReLU) activation function
$$  f(x) =
\begin{cases}
0.01x,  & x \lt 0 \\
x, & x \geq 0 
\end{cases} $$

### Components of NN

#### Activation Function

Activation Functions determines the output of each element (perceptron or neuron) in the neural network. Each neuron’s output is the input of the neurons in the next layer of the network, so the inputs pass through multiple activation functions until the output layer gives a prediction.

#### Bias

Bias is a non-zero number defined by us and it acts the same way as $$c$$ does in the equation $$y = m\times x + c$$.

#### Neuron

A neuron is the most basic unit of a Neural Network. Each neuron stores information either as a real number or a mathematical operation that takes input, multiplies it by it's weights and then passes the sum through the activation function to the other neurons.


#### Weights

Weights decide the importance of the input coming into a neuron. Weights are initialised randomly in the beginning, later however they are automatically calculated based on the output.

### Loss Functions

#### MSE(Mean Squared Error)

#### RMSE(Root Mean Squared Error)

#### Log Loss