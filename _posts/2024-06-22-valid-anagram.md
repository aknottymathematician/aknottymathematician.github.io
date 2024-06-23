---

title: "Valid Anagram"
# header:
#   image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
excerpt_image: "/assets/images/DSA_Problems_Teaser_22-Jun-2024.jpg"
excerpt: "Valid Anagram"
# mathjax: true
# toc: true
layout: post
# author_profile: true
categories: leetcode
tags: hashmap string easy
---

## [Problem Statement](https://leetcode.com/problems/valid-anagram/description/)

Given two strings *s* and *t*, return true if *t* is an anagram of *s*, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.



 

> **Example 1:** <br />

*Input:* s = "anagram", t = "nagaram" <br />
*Output:* true

>**Example 2:** <br />
*Input:* s = "rat", t = "car"
*Output:* false


**Constraints:**
* 1 <= s.length, t.length <= 5 * 10<sup>4<sup/>
* s and t consist of lowercase English letters.



# Intuition
The intuition for this problem is very simple, we have to check all the characters in string *s* are present in string *t* and vice-versa. In other words, we just count the number of characters in each string and check if each character has the same count.

# Approach
* There are multiple ways in which this problem can be solved,
    1. Use **Counter** function in python to count number of characters in each string. The time complexity of this O(N) and space complexity is O(N) as well.
    ```python
    class Solution:
        def isAnagram(self, s: str, t: str) -> bool:
            return Counter(s) == Counter(t)
            #returns True if counts match, else returns False
    ```
    2.  Sort the strings and then it's the matter of simple exact match.
    ```python
    class Solution:
        def isAnagram(self, s: str, t: str) -> bool:
            sortedS = sorted(s)
            sortedT = sorted(t)

            if sortedS == sortedT:
                return True
            else:
                return False
    ```
    3. The third approach is to use *hashmap* to count the number of characters in each string and if they match, return True, else False.

* To elaborate more on the third approach,
    1. We first check if lengths of strings are same, if not we automatically return False.
    2. Since the lengths are same, now running the for loop on one string will suffice.
    3. We save counts of each character for strings s and t in hashmaps countS and countT respectively. We use get function for retriving elements to avoid *element not found* error.
    4. In these hashmaps, key is the character and the value is the character count in that string. 
    5. Finally we run a loop to compare counters of each key hashmap.


# Complexity
- Time complexity: O(N) where N is number of characters in strings s and t


- Space complexity: O(N) where N is numbers of characters in srings s and t


# Code for approach 3
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        countS, countT = {}, {}
        for i in range(len(s)):
            # we increment the count each time we encounter a character
            countS[i] = 1 + countS.get(s[i], 0)
            countT[i] = 1 + countT.get(t[i], 0)
        for c in countS:
            if countS[c] != countT.get(c, 0):
                return False
        return True
```


## Refrence
* [Leetcode](https://leetcode.com/problems/two-sum/solutions/)