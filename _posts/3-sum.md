---

title: "3Sum"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "3Sum"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/3sum/)

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.


> **Example 1:** <br />
*Input:* nums = [-1,0,1,2,-1,-4]<br />
*Output:* [[-1,-1,2],[-1,0,1]]<br />

> **Example 2:**
*Input:* s = []
*Output:* []<br />

> **Example 3:**
*Input:* s = [0]
*Output:* []<br />


**Constraints:**
* 0 <= nums.length <= 3000
* -10<sup>5</sup> <= nums[i] <= 10<sup>5</sup>

## Approach

This problem is similar to 2Sum problem, but here we need to find sums of three elements. We can use similar idea with hash-tables, but the problem here is that we can have duplicates, and it is a bit painful to deal with them, using hash-tables, we need to count frequencies, make sure, we did not use the same elements and so on.

Another approach is to use 2 Pointers approach. Let us sort our data first and choose element number i. What we need to find now is some elements with indexes beg and end, such that i < beg < end and nums[beg] + nums[end] = target = -nums[i]. Here times come to use our 2 Pointers approach: we start from beg, end = i + 1, n - 1, and move beg to the right and end to the left, comparing nums[beg] + nums[end] with our target. If it is equal to target, we add it to our result, and move two pointers. However, because we can have equal numbers in nums, we still need to check, that we return unique triples, so we apply set in the end.



## Solution
```python
def threeSum(arr):
    arr.sort()
    sums = []
    n = len(arr)

    for i in range(n):
        if i>0 and arr[i]==arr[i+1]:
            continue
        target = -arr[i]
        start = i+1
        end = n-1

        while start<end:
            if arr[start]+arr[end] == target:
                sums.append((arr[i], arr[start], arr[end]))
                start += 1
                end -= 1
            elif arr[start]+arr[end] < target:
                start+=1
            else:
                end-=1
    
    return set(sums)

```



## Conclusion
Time complexity is O(n log n + n^2) = O(n^2), because we sorted our data, and then we have loop with n iterations, inside each of them we use 2 pointers approach with O(n) complexity (inside while beg < end: each time distance between our pointers reduced by at least 1). Space complexity is potentially O(n^2), because there can be potentially O(n^2) solutions:

let nums = [-n,-n+1,..., n-1, n] with 2n+1 = O(n) numbers, then there will be solutions: 1 2 -3, 1 3 -4, … , 1 n-1 -n 2 3 -5, 2 4 -6, … , 2 n-2 -n

in first group there will be n-2 solutions, in second n-4 and so on. Sum of arithmetic progression n-2 + n-4 + ... is approximately equalt to n^2/4. We also have more solutions, but we already showed that there is O(n^2).


## Refrence
* [Dmitry](https://flykiller.github.io/leetcode/0015.html)