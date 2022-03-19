---

title: "Remove Duplicate Letters"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Remove Duplicate Letters"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/remove-duplicate-letters/)

Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.
> **Example 1:** <br />
*Input:* s = "bcabc"<br />
*Output:* "abc"<br />

> **Example 2:**
*Input:* s = "cbacdcbc"
*Output:* "acdb"<br />


**Constraints:**
* 1 <= s.length <= 104
* s consists of lowercase English letters.

## Approach

Even before starting to solve one important point to note is that, we want to remove duplicates and maintain lexicography order. Implying, the final answer should be lexicographically smallest while containing all unique alphabets.

> Which Data Structure do we use in order to solve this problem??<br />
We start by picking the character if it is not already visited. We'll also make sure, the previously picked character is smaller than the current character in order to maintain lexicographically order. So, how do we know which the operation to perform with previously picked character, by using **Stack**

Let us try to build our answer in greedy way: we take alphabets one by one and put them into stack: if the next alphabets in the string is in decreased lexicographical order, we **pop** it from stack and replace it with new alphabet. However we need to be careful: if we remove some alphabet from the stack and it was it's last occurence in the input string, we don't satisfy the condition that all unique alphabets must be in the output. 

* Find last_occ: last occurences for each letter in our string
* Initialize our stack either as empty or with symbol, which is less than any letter (‘!’ in my case), so we do not need to deal with the case of empty stack. Also initialize Visited as empty set.
* Iterate over our string and if we already have symbol in Visited, we just continue.
* Then, we try to remove elements from the top of our stack: we do it, if new symbol is less than previous and also if last occurence of last symbol is more than i: it means that we have removed symbol later in our string, so if we remove it we will not fail to constract full string.
* Append new symbol to our stack and mark it as visited.
* Finally, return string built from our stack.



## Solution
```python
def remove DuplicateLetters(s):
    last_occ = {c:i for i, c in enumerate(s)}
    stack = ["!"]
    visited = set()

    for i, symbol in enumerate(s):
        if symbol in visited:
            continue
        while symbol<stack[-1] and last_occ[stack[-1]]>i:
            visited.remove(stack.pop())
        
        stack.append(symbol)
        visited.add(symbol)
    return "".join(stack)[1:]

```

## Lexicographically smallest
The smallest lexicographical order is an order relation where string s is smaller than t, given the first character of s (s1) is smaller than the first character of t (t1), or in case they are equivalent, the second character, etc.

So aaabbb is smaller than aaac because although the first three characters are equal, the fourth character b is smaller than the fourth character c.

For cbacdcbc, there are several options, since b and c are duplicates, you can decided which duplicates to remove. This results in:

> cbacdcbc = adbc <br />
cbacdcbc = adcb<br />
cbacdcbc = badc<br />
cbacdcbc = badc<br />
...<br />

since adbc < adcb, you cannot thus simply answer with the first answer that pops into mind.


## Conclusion
Time complexity is O(n), because we iterate our string once.<br /> Space complexity is O(26), because it will be the longest size of our stack and answer.

## Refrence
* [Dmitry](https://flykiller.github.io/leetcode/0316.html)
* [Leetcode](https://leetcode.com/problems/remove-duplicate-letters/discuss/1859410/JavaC%2B%2B-DETAILED-%2B-VISUALLY-EXPLAINED-!!)
* [Stack Overflow](https://stackoverflow.com/questions/34531748/how-to-get-the-smallest-in-lexicographical-order)