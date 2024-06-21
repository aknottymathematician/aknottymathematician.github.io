---

title: "Search in Rotated Sorted Array"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Search in Rotated Sorted Array"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/search-in-rotated-sorted-array/)

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.


> **Example 1:** <br />
*Input:* nums = [4,5,6,7,0,1,2], target = 0<br />
*Output:* 4<br />

> **Example 2:**
*Input:* nums = [4,5,6,7,0,1,2], target = 3<br />
*Output:* -1<br />

**Constraints:**
* 1 <= nums.length <= 5000
* -10<sup>4<sup/> <= nums[i] <= 10<sup>4<sup/>
* All values of nums are unique.
* nums is an ascending array that is possibly rotated.
* -10<sup>4<sup/> <= target <= 10<sup>4<sup/>



## Approach I (Iterative)

We need to use a variant of binary search which will take care of rotation.

**Complexity**: Time complexity is O(logN), space complexity is O(1).


## Solution I
```python

def search(arr, target):
    start = 0
    end = len(arr)-1

    while start <= end:
        mid = start + (end-start)//2

        if arr[mid] == target:
            return mid
        #if left array is sorted
        if arr[start]<=arr[mid]:
            if arr[start]<=target<arr[mid]:
                end = mid-1
            else:
                start = mid + 1
        #if right array if sorted
        elif arr[mid] <= arr[end]:
            if arr[mid]<=target <arr[end]:
                start = mid+1
            else:
                end = mid-1
    return -1

```

## Approach II (Recursive)

We need to use a variant of binary search which will take care of rotation.

Divide array into 2 halves and understand, which part you should choose. Let us use dfs(beg, end) function, which will look inside region from beg to end. Then we check condition nums[mid] > nums[end] and if it is the case, we check where target is and decide to which half we need to go. Similar logic in another case. Look at examples [3,4,5,6,1,2] and [5,6,1,2,3,4] to understand what cases we can have.

**Complexity**: Time complexity is O(logN), space complexity is O(1).


## Solution II

```python
def search(arr, target):
    start = 0
    end = len(arr)-1

    def helper(start, end):
        if end-start <= 1:
            if arr[start] == target: return start
            if arr[end] == target: return end
            return -1
        
        mid = start + (end-start)//2

        if arr[mid] > arr[end]:
            if arr[end]< target <=arr[mid]:
                return helper(start, mid)
            else:
                return helper(mid, end)
        else:
            if arr[mid]<target<=arr[end]:
                return helper(mid, end)
            else:
                return helper(start, mid)
    return helper(start, end)

```
## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/0033.html)