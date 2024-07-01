---

title: "Find First and Last Position of Element in Sorted Array"
# header:
#   image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
excerpt_image: "/assets/images/DSA_Problems_Teaser_22-Jun-2024.jpg"
excerpt: "Find First and Last Position of Element in Sorted Array"
# mathjax: true
# toc: true
layout: post
# author_profile: true
categories: leetcode
tags: array binarysearch medium
---

## [Problem Statement](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.


 

> **Example 1:** <br />

*Input:* nums = [5,7,7,8,8,10], target = 8 <br />
*Output:* [3,4]

>**Example 2:** <br />
*Input:* nums = [5,7,7,8,8,10], target = 6 <br />
*Output:* [-1,-1]

>**Example 2:** <br />
*Input:* nums = [], target = 0 <br />
*Output:* [-1,-1]


**Constraints:**
* 1 <= nums.length <= 10<sup>5<sup/>
* -10<sup>9<sup/> <= nums[i] <= 10<sup>9<sup/>
* -10<sup>9<sup/> <= target <= 10<sup>9<sup/>
* nums is a non-decreasing array.



## Approach(Binary Search)

Given that the array is non-decreasing and expected time complexity is O(log n) we can use Binary Search.
* The idea is here is that along with normal binary search algorithm where we return the, so called, "mid" index value on which the target exists in the array, we also need to consider two variables *first* and *last* which will basically tell us the occurences of target.

* Now, for first occurence, whenever we find nums[mid] which is equal to target we assign **first = mid** while assigning **end = mid-1** knowing that if mid is already not the first occurence, it will be to the left of the mid. Rest of Binary Search algorithm remains the same since the search is still on for the mid such that *nums[mid]==target*

* For last occurence, the approach remains the same, except when we actually find the mid such that *nums[mid]==target*, we assign **last = mid** while assigning **start = mid + 1** knowing that last occurence of targe if not at mid will be after mid.


## Solution I
```python
def binarySearch(nums, target):
    start, end = 0, len(nums)-1
    first, last = -1, -1

    while first<=last:
        mid = (start+end)//2

        if nums[mid] == target:
            first = mid
            end = mid-1
        elif nums[mid]<target:
            start = mid+1
        else:
            end = mid-1
    start, end = 0, len(nums)-1
    while start <= end:
        mid = (start+end)//2
        
        #second occurence
        if nums[mid]==target:
            last = mid
            start = mid+1
        elif nums[mid]<target:
            start = mid+1
        else:
            end = mid-1
    return [first, last]


```


**Complexity**: Time complexity is O(log(N)) and space complexity is O(1)




## Refrence
* [Leetcode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/solutions/)