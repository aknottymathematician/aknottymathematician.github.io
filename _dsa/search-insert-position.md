---

title: "Search Insert Position"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Search Insert Position"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/search-insert-position/)

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

> **Example 1:** <br />
*Input:* nums = [1,3,5,6], target = 5<br />
*Output:* 2<br />

> **Example 2:**
*Input:* nums = [1,3,5,6], target = 2<br />
*Output:* 1<br />

> **Example 2:**
*Input:* nums = [1,3,5,6], target = 7<br />
*Output:* 4<br />

**Constraints:**
* 1 <= nums.length <= 10<sup>4<sup/>
* -10<sup>4<sup/> <= nums[i] <= 10<sup>4<sup/>
* nums contains distinct values sorted in ascending order.
* -10<sup>4<sup/> <= target <= 10<sup>4<sup/>


## Approach I

In this solution we use an inbuilt python library called **bisect**. More about bisect at the end.
**Complexity**: Time complexity is O(logn), space complexity is O(1).


## Solution
```python

from bisect import bisect_left

def searchInsert(nums, target):
    return bisect_left(nums, target)

```

## Approach II

In second approach, we use binary search with a small twist of returning *start* pointer instead of -1 in case element is not found.

**Complexity**: Time complexity is O(logn), space complexity is O(1).


## Solution
```python

def searchInsert(nums, target):
    start = 0
    end = len(nums)-1

    while start <= end:
        # to avoid overflow
        mid = start + (end-start)//2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            start = mid+1
        else:
            end = mid-1
    
    return start

```


## Bisect
The purpose of Bisect algorithm is to find a position in list where an element needs to be inserted to keep the list sorted.

1. bisect(list, num, beg, end) :- This function returns the position in the sorted list, where the number passed in argument can be placed so as to maintain the resultant list in sorted order. If the element is already present in the list, the right most position where element has to be inserted is returned. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.

2. bisect_left(list, num, beg, end) :- This function returns the position in the sorted list, where the number passed in argument can be placed so as to maintain the resultant list in sorted order. If the element is already present in the list, the left most position where element has to be inserted is returned. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.

3. bisect_right(list, num, beg, end) :- This function works similar to the “bisect()” and mentioned above.

## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/0035)
* [GFG](https://www.geeksforgeeks.org/bisect-algorithm-functions-in-python/)
* [Scaler Topics](https://www.scaler.com/topics/data-structures/insertion-sort/)
