---

title: "Validate Stack Sequences"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Validate Stack Sequences"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/validate-stack-sequences/)

Given two integer arrays pushed and popped each with distinct values, return true if this could have been the result of a sequence of push and pop operations on an initially empty stack, or false otherwise.

> **Example 1:** <br />
*Input:* pushed = [1,2,3,4,5], popped = [4,5,3,2,1]<br />
*Output:* true<br />
*Explanation:* We might do the following sequence:<br />
push(1), push(2), push(3), push(4),<br />
pop() -> 4,<br />
push(5),<br />
pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1<br />

> **Example 2:**
*Input:* pushed = [1,2,3,4,5], popped = [4,3,5,1,2]<br />
*Output:* false<br /><br />
Explanation: 1 cannot be popped before 2.<br />


**Constraints:**
* 1 <= pushed.length <= 1000
* 0 <= pushed[i] <= 1000
* All the elements of pushed are unique.
* popped.length == pushed.length
* popped is a permutation of pushed.

## Approach

Let us use iterate through pushed and popped and on each step we decide what we need to do. Consider example
pushed = [1, 2, 3, 4, 5], popped = [4, 5, 3, 2, 1]. Let ind1 and ind2 be indexes in these lists.

1. ind1 = 0 and ind2 = 0. Stack is empty so far, so all we can do is to push elements, so stack = [1] now, increment ind1.
2. ind1 = 1 and ind2 = 0. We check if we can pop element from stack right now. The reason that we want to pop as soon as possible, that all elements in popped (and pushed) are different, so if we miss the moment of time when we need to pop, we never do it after. So we check condition stack and stack[-1] == popped[ind2] and if it is false, we pop element. It is not the case here, so we push element to stack and increment ind1, stack = [1, 2].
3. ind1 = 2 and ind2 = 0, similar logic, increment ind1 and stack = [1, 2, 3].
4. ind1 = 3 and ind2 = 0, similar logic, increment ind1 and stack = [1, 2, 3, 4].
5. ind1 = 4 and ind2 = 0. Now, we have popped[ind2] = 4, which is equal to the top of our stack, so we pop it from stack and increment ind2, stack = [1, 2, 3].
6. ind1 = 4 and ind2 = 1. We increment ind1 and stack = [1, 2, 3, 5].
7. ind1 = 5 and ind2 = 1. Top of stack equal to popped[ind2], so we pop element and increment ind2, stack = [1, 2, 3]
8. ind1 = 5 and ind2 = 2. Same logic, we increment ind2 and stack = [1, 2]
9. ind1 = 5 and ind2 = 3. Same logic, we increment ind2 and stack = [1]
10. ind1 = 5 and ind2 = 4. Same logic, we increment ind2 and stack = []
11. ind1 = 5 and ind2 = 5, so we do not go inside while statement.

> Note also, that we need to ckeck condition ind1 < n, that is we can push element to stack. If not, then we can immedietly return False. In the end, if we reached it we return True.


## Solution
```python
def validate(pushed, popped):
    stack = []
    idx1 = 0
    idx2 = 0
    n = len(pushed)

    while idx1 < n or idx2 < n:
        if stack and stack[-1] = popped[idx2]:
            stack.pop()
            idx2+=1
        elif idx1 < n:
            stack.append(pushed[idx1])
            idx1+=1
        else:
        return False
    return True


```

## Conclusion
Time and Space Complexity both are O(N) where N is length of the string.<br />
Reason for that is there is one pass over the string and stack of maximum length N.

## Refrence
* [Leetcode](https://leetcode.com/problems/validate-stack-sequences/discuss/1083489/Python-Two-pointers-simulate-stack-explained)