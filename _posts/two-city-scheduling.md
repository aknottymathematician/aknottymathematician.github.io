---

title: "Two City Scheduling"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Two City Scheduling"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/boats-to-save-people/)

A company is planning to interview 2n people. Given the array costs where costs[i] = [aCosti, bCosti], the cost of flying the ith person to city a is aCosti, and the cost of flying the ith person to city b is bCosti.

Return the minimum cost to fly every person to a city such that exactly n people arrive in each city.

> **Example 1:** <br />
*Input:* costs = [[10,20],[30,200],[400,50],[30,20]]<br />
*Output:* 110<br />
*Explanation:* The first person goes to city A for a cost of 10.<br />
The second person goes to city A for a cost of 30.<br />
The third person goes to city B for a cost of 50.<br /> 
The fourth person goes to city B for a cost of 20.<br />
The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.

> **Example 2:**
*Input:* costs = [[259,770],[448,54],[926,667],[184,139],[840,118],[577,469]]<br />
*Output:* 1859<br /><br />

> **Example 3:**
*Input:* costs = [[515,563],[451,713],[537,709],[343,819],[855,779],[457,60],[650,359],[631,42]]<br />
*Output:* 3086<br /><br />
Explanation:  4 boats (3), (3), (4), (5)<br />


**Constraints:**
* 2 * n == costs.length
* 2 <= costs.length <= 100
* costs.length is even.
* 1 <= aCosti, bCosti <= 1000


## Approach

Let us first send all the people to the first city. Now, we need to choose half of them and change their city from first to second. Which ones we need to choose? Obviously the half with the smallest difference of costs between second and first cities. This difference can be negative and positive. Let us go through example: costs = [[10,20],[30,200],[400,50],[30,20]] Then:

* We put all of them to 1 city and pay 10 + 30 + 400 + 30
* Now, evaluate differences: 10, 170, -350, -10.
* Choose 2 smallest differences, in this case it is -350 and -10 (they are negative, so we can say we get a refund)
* Evaluate final sum as 10 + 30 + 400 + 30 + -350 + -10 = 110

**Complexity**: O(n log n), because we need to make one sort, and O(n) for evaluating differences and two sums. Space complexity is O(n), because we need to keep array of differences.


## Solution
```python

def twoCitySchedCost(costs):
    firstCity = [i for i, j in costs]
    diffCity = [j-i for i, j in costs]

    return sum(firstCity) + sum(sorted(diffCity)[:len(costs)//2])

```

## Conclusion
There are some amazing explanations [here](https://leetcode.com/problems/two-city-scheduling/discuss/278716/C++-O(n-log-n)-sort-by-savings/265369) and [here](https://leetcode.com/problems/two-city-scheduling/discuss/1881240/JavaC%2B%2B-THE-EASIEST-EXPLANATION)

## Refrence
* [FlyKiller](https://flykiller.github.io/leetcode/1029)