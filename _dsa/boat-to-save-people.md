---

title: "Boats to Save People"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Boats to Save People"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/boats-to-save-people/)

You are given an array people where people[i] is the weight of the ith person, and an infinite number of boats where each boat can carry a maximum weight of limit. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most limit.

Return the minimum number of boats to carry every given person.

> **Example 1:** <br />
*Input:* people = [1,2], limit = 3<br />
*Output:* 1<br />
*Explanation:* 1 boat (1, 2)<br />

> **Example 2:**
*Input:* people = [3,2,2,1], limit = 3<br />
*Output:* 3<br /><br />
Explanation:  3 boats (1, 2), (2) and (3)<br />

> **Example 3:**
*Input:* people = [3,5,3,4], limit = 5<br />
*Output:* 4<br /><br />
Explanation:  4 boats (3), (3), (4), (5)<br />


**Constraints:**
* 1 <= people.length <= 5 * 104
* 1 <= people[i] <= limit <= 3 * 104


## Brute Force Approach

Given an array we use 2 pointers.
* One of them starting from 0th index and another from 1st index. We gonna have one count variable as well, which helps us in get the no. of count of boats.
* Sum them up & if their weight is less than or equals to limit, then increment the count otherwise increment the 1st index pointer, until we find less then or equal to the limit
* If unable to find anyone of them, we gonna increment the count of 0th index pointer

Because we are re-visiting the character which we have already visited & we are recalculating it, it not the most optimal approach.

Time Complexity will be O(N^2)


## Optimal Approach

The key intuition here is that:
* Every person must be saved.
* For each person it is better to find another person with biggest weight, such that sum of their weights is no more than limit. Indeed, if we put another person, we will have subproblem A, which is always worse than if we put biggest one (subproblem B): every solution of B can be also used to solve A as well, but not the opposite.

So, let us sort our people by weight and use two pointers technique to allocate them to boats:

* If people[beg] + people[end] <= limit, then we can put these two persons in one boat, so we move beg to the right, end to the left and increment ans by one.
* In opposite case it means, that person with smallest weight and with biggest weight so far can not be put in one boat, so, we need to decrease weight: movint end pointer one step to the left.

**Complexity**: time complexity is O(n log n), because we sorted our data and then we have O(n) for two-pointers approach. Space complexity is O(n).

## Solution
```python

def numRescueBoats(people, limit):
    people.sort()
    start, end = 0, len(people)-1
    ans =0

    while start<=end:
        if people[start]+people[end]:
            start += 1
        
        end-=1
        ans += 1

    return ans

```

## Conclusion
This is quite a simple problem, the follow-up for this problem will be, [**what if more than two people could sit in one boat?**](https://leetcode.com/problems/boats-to-save-people/discuss/156740/C%2B%2BJavaPython-Two-Pointers)

## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/0881)