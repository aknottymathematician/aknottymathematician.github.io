---
title: "Python Code"
date: 2020-08-16
tags: [python]
header:
  image: "/assets/images/blog-head-neural-network_16-August-2020.jpg"
excerpt: "Python Coding"
mathjax: "true"

---

# Code to add two numbers

Here we see three ways to add two numbers. Two using functions one without functions -  

- Method 1
```python
    import numpy as np
    
    def function_using_numpy(x,y):
      z = np.sum(x,y)
      return z
```
- Method 2
```python

	def function_without_using_numpy(x,y):
		z = x+y
		return z
```

- Method 3
```python

	x = 9
	y = 10

	z = x+y
```
