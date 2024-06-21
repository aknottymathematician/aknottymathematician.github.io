---

title: "Valid Palindrome II"
# header:
#   image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
#   teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Valid Palindrome II"
# mathjax: true
# toc: true
layout: post
# author_profile: true
categories: leetcode
tags: [string]
---

## [Problem Statement](https://leetcode.com/problems/valid-palindrome-ii/)

Given a string s, return true if the s can be palindrome after deleting at most one character from it.


> **Example 1:** <br />
*Input:* s = "abca"<br />
*Output:* true<br />

> **Example 2:**
*Input:* s = "abc"<br />
*Output:* false<br />

**Constraints:**
* 1 <= s.length <= 10<sup>5<sup/>
* s consists of lowercase English letters.


## Approach I

Create a helper function checkPalindrome that takes a string s, and two pointers i and j. This function returns a boolean indicating if s.substring(i, j) is a palindrome. Implementation details for this function can be found in the first section of this article.

Initialize two pointers, i = 0 and j = s.length() - 1.

While i < j, check if the characters at indices i and j match. If they don't, that means we must spend our deletion on one of these characters. Try both options using checkPalindrome. In other words, return true if either checkPalindrome(s, i, j -1) or checkPalindrome(s, i + 1, j) is true.

If we exit the while loop, that means the original string is a palindrome. Since we didn't need to use the deletion, we should return true.

**Complexity**: 
Given N as the length of s,

Time complexity: O(N).

The main while loop we use can iterate up to N / 2 times, since each iteration represents a pair of characters. On any given iteration, we may find a mismatch and call checkPalindrome twice. checkPalindrome can also iterate up to N / 2 times, in the worst case where the first and last character of s do not match.

Because we are only allowed up to one deletion, the algorithm only considers one mismatch. This means that checkPalindrome will never be called more than twice.

As such, we have a time complexity of O(N).

Space complexity: O(1).

The only extra space used is by the two pointers i and j, which can be considered constant relative to the input size.


## Solution I
```python

def validPalindrome(s):
    def check(s, i, j):
        while i < j:
            if s[i] != s[j]:
                return False
            i+=1
            j-=1
        return True
    i = 0
    j = len(s)-1

    while i<j:
        if s[i]!=s[j]:
            return check(s,i, j+1) or check(s,i+1,j)
        i+=1
        j-=1
    return True

```


## Refrence
* [Leetcode](https://leetcode.com/problems/valid-palindrome-ii/solution/)