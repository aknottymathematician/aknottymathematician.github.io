---

title: "Maximum Frequency Stack"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Maximum Frequency Stack"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/maximum-frequency-stack/)

Design a stack-like data structure to push elements to the stack and pop the most frequent element from the stack.

Implement the FreqStack class:

* FreqStack() constructs an empty frequency stack.
* push(val) pushes an integer val onto the top of the stack.
* pop() removes and returns the most frequent element in the stack.
* If there is a tie for the most frequent element, the element closest to the stack's top is removed and returned.

> **Example 1:** <br />
*Input:* ["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"]
[[], [5], [7], [5], [7], [4], [5], [], [], [], []]<br />
*Output:* [null, null, null, null, null, null, null, 5, 7, 5, 4]<br />
*Explanation:* <br />
FreqStack freqStack = new FreqStack();<br />
freqStack.push(5); // The stack is [5]<br />
freqStack.push(7); // The stack is [5,7]<br />
freqStack.push(5); // The stack is [5,7,5]<br />
freqStack.push(7); // The stack is [5,7,5,7]<br />
freqStack.push(4); // The stack is [5,7,5,7,4]<br />
freqStack.push(5); // The stack is [5,7,5,7,4,5]<br />
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,5,7,4].<br />
freqStack.pop();   // return 7, as 5 and 7 is the most frequent, but 7 is closest to the top. The stack becomes [5,7,5,4].<br />
freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,4].<br />
freqStack.pop();   // return 4, as 4, 5 and 7 is the most frequent, but 4 is closest to the top. The stack becomes [5,7]. <br />


**Constraints:**<br />
* 0 <= val <= 109
* At most 2 * 104 calls will be made to push and pop.
* It is guaranteed that there will be at least one element in the stack before calling pop.

## Approach 1 : using SortedList
There is solution with complexity O( log n) for pop and push. We will keep 3 pieces of information:

1. **self.SList** is sorted list, where we keep tuples of 3 numbers: frequency, number itself and biggest index we have for this number.
2. **self.Places** is defaultdict, where for each num we keep all indexes.
3. **self.N** number of element we push into our data structure. Note, that we do not decrease this number, only increase. Because when we pop the element we return element with max frequency and not the one at the top of the stack.

Now, how function will work:

**push(self, x)**: first, we check frequency of new element and update it: we remove tuple from our sorted list and put updated frequency. We also add new index to self.Places[x] and update self.N<br />
**pop(self)**: we pop last element from our sorted list: it will be what we wanted. If frequency of extracted element is 2 or more, than we need to put element with updated frequency to our sorted list. Also we remove last element from self.Places.

**Conclusion**
Since we are using SortedList() the time complexity of all operations will be O(logN)


## Solution
```python
from sortedcontainers import SortedList
class FreqStack:
    def __init__(self):
        self.SList = SortedList()
        self.PLaces = defaultdict(list)
        self.N = 0
    
    def push(self, val):
        #checking frequency of new element
        freqVal = len(self.Places[val])
        #if element already exists
        if freqVal > 0:
            #remove the tuple(freqeuncy, biggest index and number itself) from SList
            self.SList.remove((freqVal, self.Places[val][-1], val))
        #if it doeesn't or after handling the case of existence
        self.SList.add((freqVal+1, self.N, val))
        self.Places[val].add(self.N)
        self.N += 1
    
    def push(self):
        
    



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