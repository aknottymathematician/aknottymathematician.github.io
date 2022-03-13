---

title: "Most Frequent Number follwoing a Key in Array"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Most Frequent Number follwoing a Key in Array"
mathjax: true
toc: true
author_profile: true
---


# [Problem Statement](https://leetcode.com/problems/most-frequent-number-following-key-in-an-array/)
You are given a 0-indexed integer array nums. You are also given an integer key, which is present in nums.

For every unique integer target in nums, count the number of times target immediately follows an occurrence of key in nums. In other words, count the number of indices i such that:

> 0 <= i <= nums.length - 2,<br />
nums[i] == key and,<br />
nums[i + 1] == target.

Return the target with *the maximum count*. The test cases will be generated such that the target with maximum count is unique.

>**Constraints:**<br />
2 <= nums.length <= 1000<br />
1 <= nums[i] <= 1000<br />
The test cases will be generated such that the answer is unique.


## Solution I
```python
from Collections import Counter

def mostFrequent(nums):
    count = Counter()
    for i, n in enumerate(nums):
        if n == key and i<len(nums)-1:
            count[nums[i+1]] += 1
    
    return count.most_common()[0][0]
```

## Solution II
```python
def mostFrequent(arr, key):
    num = [0]*1001
    for i in range(len(arr)-1):
        if arr[i] == key:
            num[arr[i+1]] += 1
    
    return num.index(max(num))

```

## Conclusion
Time Complexity is O(N) for one pass of list and Space Complexity is O(N) for creating hashmap.