---

title: "Binary Search"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Binary Search"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/binary-search/)

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

> **Example 1:** <br />
*Input:* nums = [-1,0,3,5,9,12], target = 9<br />
*Output:* 4<br />

> **Example 2:**
*Input:* nums = [-1,0,3,5,9,12], target = 2<br />
*Output:* -1<br />


**Constraints:**
* 1 <= nums.length <= 10<sup>4<sup/>
* -10<sup>4<sup/> <= nums[i] <= 10<sup>4<sup/>
* All the integers in nums are unique.
* nums is sorted in ascending order.

## Approach I

First approach is an iterative where while look is used to sort through the list.

**Complexity** for this method is O(logN) since we halve the length of list with each iteration.


## Solution
```python

def binarySearch(nums, target):
    start = 0
    end = len(nums)-1

    while start <= end:
        mid = start + (end- start)/2
        if nums[mid] == target:
            return mid
        
        elif nums[mid] < target:
            end = mid-1
        
        else:
            start = mid+1
    return -1

```

## Approach II

In second approach, we use recusion to write binary search function.

**Complexity**: Time complexity is O(logn), space complexity is O(1).


## Solution
```python

def binarySearch(nums,start, end, target):
    if start <= end:
        # to avoid overflow
        mid = start + (end-start)//2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            return binarySearch(nums, mid+1, end, target)
        else:
            return binarySearch(nums, start, mid-1, target)
    
    return -1

```


## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/0704)