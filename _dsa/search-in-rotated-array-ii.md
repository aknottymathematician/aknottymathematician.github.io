---

title: "Search in Rotated Sorted Array II"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Search in Rotated Sorted Array II"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/search-in-rotated-sorted-array/)

There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.


> **Example 1:** <br />
*Input:* nums = [2,5,6,0,0,1,2], target = 0<br />
*Output:* true<br />

> **Example 2:**
*Input:* nums = [2,5,6,0,0,1,2], target = 3<br />
*Output:* false<br />

**Constraints:**
* 1 <= nums.length <= 5000
* -10<sup>4<sup/> <= nums[i] <= 10<sup>4<sup/>
* All values of nums are unique.
* nums is an ascending array that is possibly rotated.
* -10<sup>4<sup/> <= target <= 10<sup>4<sup/>



## Approach I (Iterative)

We need to use a variant of binary search which will take care of rotation and duplicate values.

To solve this problem we have to follow the folllowing steps:

Calculate the mid index.
Check if the mid element == target, return True else move to next step.
Else if the mid element >= left.
if mid element >= target and and left <= target, then shift right to mid-1 position, else shift left to mid+1 position.
Else,
If target >= mid element and target <=right, then shift left to mid+1 position, else shift right to mid-1 position.
If the element is not found return False
Note: Since duplicate elemnts are present in the array so remove all the duplicates before step step 1.
To remove duplicate,

Shift left while left == left+1, and
Shift right while right == right-1.

**Complexity**: if we do not have any duplicates, it is for sure O(log n). If we have any, it can be potentially O(n) for cases like 111111111111121111: where we do not know the place of 2 and we basically need to traverse all elements to find it.


## Solution I
```python

def search(arr, target):
    start = 0
    end = len(arr)-1

    while start <= end:

        while start < end and arr[start] == arr[start+1]:
            start+=1
        while start < end and arr[end] == arr[end-1]:
            end-=1
        mid  = start + (end-start)//2

        if arr[mid] == target:
            return True

        if arr[mid]>arr[end]:
            if arr[end]<target<=arr[mid]:
                end = mid-1
            else:
                start = mid+1
        else:
            if arr[start]<target<=arr[mid]:
                end = mid-1
            else:
                start = mid+1
    return False

```

## Approach II (Recursive)

The idea here is to use both binary search and dfs: each time we compare nums[mid] and nums[end] and we can have several options:

1. nums[mid] > nums[end], for example data can look like 3,4,5,6,7,1,2. Then we need to check conditions: a. If nums[end] < target <= nums[mid], then it means, that we need to look in the left half of our data: see region 1 on the left image. b. Else means, that we need to look in the right half of data.
2. nums[mid] < nums[end], for example data can look like 6,7,1,2,3,4,5. Then we need to check conditions: a. if nums[mid] < target <= nums[end], then it means, that we need to look in the right half of our data: see region 1 on the right image. b. Else means, that we need to look in the left half of data.
3. In this problem it can happen, that nums[mid] == nums[end], and in this case we do not know where to find our number, so we just look for it in both halves.

**Complexity**: if we do not have any duplicates, it is for sure O(log n). If we have any, it can be potentially O(n) for cases like 111111111111121111: where we do not know the place of 2 and we basically need to traverse all elements to find it.


## Solution II

```python
def search(arr, target):
    start = 0
    end = len(arr)-1

    def helper(start, end):
        if end-start<=1: return target in arr[start:end+1]

        mid = start+(end-start)//2

        if arr[mid]>arr[end]:
            if arr[end]<target<=arr[mid]:
                return helper(start, mid)
            else:
                return helper(mid+1, end)
        elif arr[mid]<arr[end]:
            if arr[mid]<target<=arr[end]:
                return helper(mid+1, end)
            else:
                return helper(start, mid)
        else:
            helper(start, mid) or helper(mid+1, end)
    return helper(start, end)

```
## Refrence
* [Leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/discuss/1890363/python-or-binary-search-or-explained-or)
* [FlyKiller](https://flykiller.github.io/leetcode/0081.html)