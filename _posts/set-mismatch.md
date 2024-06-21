---

title: "Set Mismatch"
# header:
#   image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
#   teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Set Mismatch"
mathjax: true
toc: true
# author_profile: true
layout: post
# title: Test markdown
# subtitle: Each post also has a subtitle
categories: markdown
tags: [set][array]
---

## [Problem Statement](https://leetcode.com/problems/set-mismatch/)

You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

> **Example 1:** <br />
*Input:* nums = [1,2,2,4]<br />
*Output:* [2,3]<br />

> **Example 2:**
*Input:* nums = [1,1]<br />
*Output:* [1,2]<br />

**Constraints:**
* 1 <= nums.length <= 10<sup>4<sup/>
* 1 <= nums[i] <= 10<sup>4<sup/>


## Approach I (Iterative)

Even though a seemingly easy problem, uses a bit of logic. What needs to be understood is 
1. The first element to be returned is difference between array and it's set, that will give us the duplicate number.
2. The second number is the one that is supposedly missing, that can be found by removing sum of set from the total of **1 to n**.

**Complexity**: Time and Space complexities are O(N).


## Solution I
```python

def setMismatch(arr):
    n = len(arr)
    return [sum(arr)-sum(set(arr)), (n*(n+1)//2)-sum(set(arr))]

```


## Refrence
* [Leetcode](https://leetcode.com/problems/set-mismatch/discuss/105558/Oneliner-Python)