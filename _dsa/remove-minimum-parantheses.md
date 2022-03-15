---

title: "Remove Minimum Parantheses"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Remove Minimum Parantheses"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

Given a string s of '(' , ')' and lowercase English characters.

Your task is to remove the minimum number of parentheses ( '(' or ')', in any positions ) so that the resulting parentheses string is valid and return any valid string.

Formally, a parentheses string is valid if and only if:

It is the empty string, contains only lowercase characters, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.

> **Example 1:** <br />
*Input:* path = s = "lee(t(c)o)de)"<br />
*Output:* "lee(t(c)o)de"<br />
*Explanation:* "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.<br />

> **Example 2:**
*Input:* s = "a)b(c)d"<br />
*Output:* "ab(c)d"<br />

> **Example 3:**
*Input:* s = "))(("<br />
*Output:* ""<br />


**Constraints:**
* 1 <= s.length <= 105
* s[i] is either'(' , ')', or lowercase English letter.


## Approach
A classic **Stack** problem.

* Convert input string to list, it'll be easier to access the elements using index.
* Lopping through the string list.
* If the element is **(** we append it in the stack.
* Else if it's **)** then we check if top indexed element from stack in the string is **(** and if it is we pop the index from stack.
* Else we append it to the stack.
* Finally we delete the elements from string which are at indices stored in stack.
* Return String.


## Solution
```python
def simplifyPath(string):
    stack = []
    string = list(string)

    for i in range(len(string)):
        if string[i] == "(":
            stack.append(i)
        elif string[i] == ")":
            if stack and string[stack[-1]]=="(":
                stack.pop()
            else:
                stack.append(i)
        while stack:
            del string[stack[-1]]
            stack.pop()
        
        return "".join(string)


```

## Conclusion
Time and Space Complexity both are O(N) where N is length of the string.<br />
Reason for that is there is one pass over the string and stack of maximum length N.

## Refrence
* [Code with Alisha](https://www.youtube.com/watch?v=wsikPyz0lGo)