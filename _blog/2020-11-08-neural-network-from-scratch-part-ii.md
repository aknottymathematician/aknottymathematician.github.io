---

title: "Neural Network from scratch - Part II"
date: 2020-10-28
comments: true
author_profile: false
related: true
share: true
read_time: true
header:
  image: "/assets/images/NN_blog-post-banner_19-October-2020.png"
  teaser: "/assets/images/KM_blog-teaser-banner-1_16-August-2020.jpg"
excerpt: "Coding the Neural Network"
mathjax: true
toc: true

---

In the first part of the **Neural Network from scratch** series we saw various components of a neural network, how each component works and the whole work flow of that architecture. If you haven't checked that already, please read through [Part I](https://aknottymathematician.github.io/nn-from-scratch-part1/).

Now to learn any concept thoroughly it is important to work examples and practice hands-on. Keeping this in mind, the agenda for the second part of this series involves studying a small example to understand the shapes of the matrices that take part in this process, then writing a neural network from scratch in python, coding a neural network using Tensorflow library and finally using the two neural networks on a dataset.





## Getting your shapes right!
As we saw previously, the whole workflow of a NN starts with the input layer. This input layer has certain number of neurons and that number is decided based on the dimension of the vector that will be taken as an input.

Let us check out an example here, say, we start a new restaurant and we want to survey if people will return to our restaurant. Now the metric of measuring is simple, a person will come back or they won't, so either 1 or 0. The parameters on which we are measuring performance of the restaurant are service quality, ambience and food quality.

||       	Input Parameters     		    ||   			 Output 	      ||
|										     | 								   |
| Service Quality | Ambience | Food Quality  |  Will the custormer come back?  |
| :-------------: | :------: | :-----------: | :-----------------------------: |
| 		7  		  | 	8    | 		7 		 | 				  1 			   |
| :-------------: | :------: | :-----------: | :-----------------------------: |
| 		5  		  | 	9    | 		4 		 | 				  0 			   |
| :-------------: | :------: | :-----------: | :-----------------------------: |
| 		8  		  | 	6    | 		9 		 | 				  1 			   |
| :-------------: | :------: | :-----------: | :-----------------------------: |
| 		2  		  | 	4    | 		9 		 | 				  0 			   |

Now here we have four users and each user has given various ratings for every parameter and then finally stated if they will come back to our restaurant. So we have in our hands a binary classification problem, where output is either 1 or 0 and we want to train a model which will tell us what is the chance of people returning to our restaurant given how they rated our parameters. We will have a single hidden layered NN, i.e. **input $$\to$$ hidden layer $$\to$$ output**.


> **_NOTE:_**  An important thing to notice here is that weights are randomly initialized in the below process.


**Layer 1 - Inputs**

We have four users with three parameters so our input matric will look like - $$\begin{bmatrix}7 \\ 8 \\ 7 \end{bmatrix}$$ (Input matrix)

which is a matrix of shape $$(3,1)$$ i.e. *3 parameters x 1 user*. Now the dimension for the weight matrix which is to be multiplied to input matrix will have shape $$(neurons, inputs)$$. So the weights matrix has the shape $$(4,3)$$ and bias matrix has the shape $$(4,1)$$. The calulation of the input layer moving forward into the hidden layer will look like - 

$$\begin{bmatrix}0.1 & -0.2 & 0.3\\-0.3 & -0.4 & 0.1\\0.7 & -0.9 & -0.1\\0.5 & -0.8 & -0.7\end{bmatrix} \times \begin{bmatrix}7 \\8\\7\end{bmatrix} + \begin{bmatrix}1 \\ 1 \\ 1 \\ 1\end{bmatrix}$$


**Layer 2 - Hidden layer**

The output matrix of the above calculation comes out as $$\begin{bmatrix}2.2\\-3.6\\-2.0\\-6.8\end{bmatrix}$$

which goes into the hidden layer as the input, where [sigmoid](https://aknottymathematician.github.io/glossary/#1-sigmoid)(can be any other too) activation function acts on the matrix to give the output

$$ A = \begin{bmatrix}0.9 \\0.027\\0.119\\0.001\end{bmatrix}$$

So the output coming from the hidden layer is the matrix $$A$$ whose shape is $$(4,1)$$. Now the weights matrix layer will have shape (1,4), 

$$\begin{bmatrix}0.5\\ 0.8\\ 0.3\\ 0.9\end{bmatrix}$$


with bias as $$\begin{bmatrix}1\end{bmatrix}$$.

**Layer 3 - Output Layer**

So, output of the hidden layer multiplied by weights plus the bias gives us the final output. That is,

$$ Output = \sigma\left(\begin{bmatrix}0.5\\ 0.8\\ 0.3\\ 0.9\end{bmatrix} \times \begin{bmatrix}0.9 \\0.027\\0.119\\0.001\end{bmatrix} + \begin{bmatrix}1\end{bmatrix}\right)$$

which gives us,
$$Output = \begin{bmatrix}0.875\end{bmatrix}$$

We "compare" this output with the given output and calculate the error. This example showed the process of FeedForward neural network, the important things to understand here are the dimensions of the matrices moving through the neural network. A quick brief recap would be,

| Input Layer | Weights1 | Bias1 |  Input/Output of hidden layer | Weights2 | Bias2 | Output Layer |
| :---------: | :-------: | :----: | :---------------------------: | :-------: | :----: | :----------: |
| 	(3,1)  	  |   (4,3)   |  (4,1) | 			(4,1)			   |	(1,4)  |   (1,)	|	   (1,)	   |


Next, based on the error we optimize the model and backpropagate and optimize the weights so that the error minimizes.

[TOP](#){: .btn .btn--danger}

Now having looked at the basics let's move on to actually writing the neural network. 

## MNIST Dataset

The dataset that I used to build the neural network on is MNIST dataset, you can more about it [here](http://yann.lecun.com/exdb/mnist/). But, in short, it is a dataset which contains images of handwritten numbers from 0 to 9. There are total of 60,000 images in the data with each image having a label of it's value and size of each image is 28x28 pixels i.e. 784 pixels for every image.

> **_NOTE:_** The images in dataset are black and white, which means pixel which has digit will be black otherwise it will be white. Had it been colour we would have 784 x 3 as the dimension of each image to compensate for three layers - RGB.

Now the idea is to build a neural network which, when given an image of handwritten number, will be able to identify the digit. I have experimented with two types of neural networks, one build using only python while the other one using tensorflow.

## Neural Network in python

To build this neural network architecture I have used only numpy and tensorflow for loading the MNIST dataset. 

The general structure of the code is as follow - 
```python
class DeepNeuralNetwork():
	def __init__(self, sizes, epochs=1, l_rate=0.001):

	def sigmoid(self, x, derivative=False):

	def softmax(self, x, derivative=False):

	def initialization(self):

	def feedforward(self, x_train):

	def backpropagation(self, y_train, output):

	def update_weights(self, change_in_weights):

	def accuracy(self, x_val, y_val):

	def train(self, x_train, y_train, x_val, y_val):

```


There are mainly 5 functions I will be going through here, feed forward, backpropagation, updating the weights, checking the accurary and then finally training the model.
### Feed Forward
In feed forward function train data is given as the input to the neural network. As seen earlier he flow is, weights matrix times input layer is passed into hidden layer which passes through the activation function.
There are three paramters here, weights(W), Inputs(A) and bias(B).
There are four layers, including input & output layer and two hidden layers.
We used two activation functions here, [Sigmoid](https://aknottymathematician.github.io/glossary/#3-sigmoid) and [Softmax](https://aknottymathematician.github.io/glossary/#6-softmax).


```python
def feedforward(self, x_train):
	
	params = self.params
	params['A0'] = x_train
	params['Z1'] = np.dot(params["W1"], params['A0']) + params['B1']
	params['A1'] = self.sigmoid(params['Z1'])
	params['Z2'] = np.dot(params["W2"], params['A1']) + params['B2']
	params['A2'] = self.sigmoid(params['Z2'])
	params['Z3'] = np.dot(params["W3"], params['A2'])+params['B3']
	params['A3'] = self.softmax(params['Z3'])

	return params['A3']
```

### Backpropagation
In the backpropagation function we calculate the error and backpropagate through the neural network to calculate weights for each possible parameter and update the weights using _update_weights_ function.

```python
def backpropagation(self, y_train, output):

	params = self.params
	change_w = {}
	error = 2 * (output - y_train) / output.shape[0] * self.softmax(params['Z3'], derivative=True)
	change_w['W3'] = np.outer(error, params['A2'])
	error = np.dot(params['W3'].T, error) * self.sigmoid(params['Z2'], derivative=True)
	change_w['W2'] = np.outer(error, params['A1'])
	error = np.dot(params['W2'].T, error) * self.sigmoid(params['Z1'], derivative=True)
	change_w['W1'] = np.outer(error, params['A0'])

	return change_w


def update_weights(self, change_in_weights):
	for key, value in change_in_weights.items():
		self.params[key] -= self.l_rate * value


```

### Training the model
Train function calls the previously defined functions and executes them of the train data. Here the model "learns" to recognise the difference between the handwritten digits.

```python
def train(self, x_train, y_train, x_val, y_val):
	
	start_time = time.time()
	for iteration in range(self.epochs):
		for x,y in zip(x_train, y_train):
			output = self.feedforward(x)
			change_in_weights = self.backpropagation(y, output)
			self.update_weights(change_in_weights)
		
		accuracy = self.accuracy(x_val, y_val)
		print('Epoch: {0}, Time Spent: {1:.2f}s, Accuracy: {2:.2f}%'.format(iteration+1, time.time() - start_time, accuracy * 100))

```



### Checking the accuracy
To check how well a neural network is trained we have the accuracy function which runs on the test data. 

```python
def accuracy(self, x_val, y_val):
	
	predictions = []
	for x, y in zip(x_val, y_val):
		output = self.feedforward(x)
		pred = np.argmax(output)
		predictions.append(pred == np.argmax(y))
	
	return np.mean(predictions)

```
Finally, we give the parameters of sizes of layers and run the code. Complete code is available in the github repository [akm_codes](https://github.com/aknottymathematician/akm_codes).

---


## Neural Network using Tensorflow

As you can see this code is much shorter and easy to read.

Unlike the previous code, where everything was manually defined, tensorflow has some amazing functions which make our lifes much easier. In the next code snippet we have defined the number of layers and the number of neurons in each layer.
```python
model = tf.keras.models.Sequential()
model.add(tf.keras.layers.Flatten())
model.add(tf.keras.layers.Dense(128, activation = tf.nn.relu))
model.add(tf.keras.layers.Dense(128, activation = tf.nn.relu))
model.add(tf.keras.layers.Dense(10, activation = tf.nn.softmax))
```
> **_NOTE:_** A model is _Sequential_ if it has linear stack of layers, which mean every layer has exactly one input and output tensor.

In the next snippet we define the parameters of the model which will decide the efficiency of the model. The parameters defined below are the default ones.

```python
model.compile(optimizer='adam',
	loss='sparse_categorical_crossentropy',
	metrics=['accuracy'])
```

Finally we fit the model on the train data or in other words train or model to "learn" the hardwritten digits. Here an important parameter is the number of epochs. Too many epochs and the model might overfit the data while, very less epochs and the model might underfit. There is no golden number for the number of epochs just like in case of number of neurons in hidden layer. We can only find the optimal number by experimenting.
```python
model.fit(x_train, y_train, epochs=3)
```
Once the model is trained we evaluate the "learning progress" of the model by testing it on the test data.

```python
val_loss, val_acc = model.evaluate(x_test, y_test)

```
If the model has overfit on trained data there is a very good chance that it's accuracy on the test data will be low. So, again, even though there is no one way of saying what accuracy is best, a rule of thumb is that train and test accuracy should be in the small neighbourhood of each other.

Complete code is available in the github repository [akm_codes](https://github.com/aknottymathematician/akm_codes).

[TOP](#){: .btn .btn--danger}

## Conclusion
So as you must have observed the neural network code using tensorlfow is much easy to understand and write. So then why put so much effort in writing one from scratch?

While going through the process of writing the whole code I went through many iterations of the code. I got to understand inner working of the neural network and realised how important it is to know the dimensions of every matrix at each step. Once you get the hang of that, experimenting and playing with hyperparameters becomes much more enjoyable.

This concludes my first series on **Neural Network from scratch**. If you find any mistake in what I have written or error in the code please drop a mail, I will do the needful as required. Until next time!

## References 

- [Sentdex](https://www.youtube.com/channel/UCfzlCWGWYyIQ0aLC5w48gBQ) YouTube channel by Harrison Kinsley

- [ML from Sratch](https://mlfromscratch.com/)

- Stanford's [CS230](https://cs230.stanford.edu/)

- [Neural Networks](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) series by Grant Sanderson

[TOP](#){: .btn .btn--danger}
