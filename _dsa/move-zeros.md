---

title: "Move Zeros"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Move Zeros"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/move-zeroes/)

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

> **Example 1:** <br />
*Input:* nums = [0,1,0,3,12]<br />
*Output:* [1,3,12,0,0]<br />

> **Example 2:**
*Input:* nums = [0]<br />
*Output:* [0]<br />


**Constraints:**
* 1 <= nums.length <= 10<sup>4<sup/>
* -2<sup>31<sup/> <= nums[i] <= 2<sup>31<sup/> - 1


## Approach

In this one of the easier problems we use two pointers, one is for current place to write number and another goes one by one through all elements.
Important thing to note that this is an in-place change problem.

**Complexity**: Time complexity is O(n), space complexity is O(1).


## Solution
```python

def moveZeros(nums):
    start, end = 0, 0
    while end<len(nums):
        if nums[end]!=0:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
        end+=1

```


## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/0283)