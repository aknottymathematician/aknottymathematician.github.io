---

title: "Find minimum in rotated sorted array"
# header:
#   image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
excerpt_image: "/assets/images/DSA_Problems_Teaser_22-Jun-2024.jpg"
excerpt: ""
# mathjax: true
# toc: true
layout: post
# author_profile: true
categories: leetcode
tags: binarysearch array medium
---

## [Problem Statement](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

* [4,5,6,7,0,1,2] if it was rotated 4 times.
* [0,1,2,4,5,6,7] if it was rotated 7 times.

> Notice that rotating an array *[a[0], a[1], a[2], ..., a[n-1]]* 1 time results in the array *[a[n-1], a[0], a[1], a[2], ..., a[n-2]]*.

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

 

> **Example 1:** <br />
*Input:* nums = [4,5,6,7,0,1,2]
*Output:* 0

>**Example 2:** <br />
*Input:* [11,13,15,17]
*Output:* 11


**Constraints:**
* 1 <= s.length, t.length <= 5 * 10<sup>4<sup/>
* s and t consist of lowercase English letters.



# Intuition
The idea is very simple, given the rotated sorted array, there will be some index for which the element is less than index+1 and index-1.


# Approach
* To look for the index for which the above mentioned condition is true, we simply have to compare *mid* to right most index element to know which direction to go in to find the minimum element.

* For that we compare *mid* element to right most element and if it's great than right most element we know that min is on that side, so we reassign start to mid+1

* If that condition is not true, which means *mid* element is less than or equal to right most element then we know our minimum element lies to the left of mid so we reassign end to mid

* We continue this process till start>=end.

 > Note <br />
 Questions to think about - <br />
    1. Why *start<end* and not *start<= end*?<br />
    2. Why *end=mid* and not *end=mid-1*?<br />
    3. Why return *end* and not *start*

# Complexity
- Time complexity: O(log(N))

- Space complexity: O(1)


# Code for approach 3
```python
def min_rotated(nums): #nums = [4,5,6,7,1,2,3]
    start = 0
    end = len(nums)-1

    while start < end:
        mid = (start+end)//2

        if nums[mid]>nums[r]:
            start = mid+1
        elif nums[mid]<=nums[r]:
            end = mid
    return nums[end]


        
```


## Refrence
* [Leetcode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/solutions/)