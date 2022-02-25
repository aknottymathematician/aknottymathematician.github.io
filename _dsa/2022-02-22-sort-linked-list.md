---

title: "Sort Linked List"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Sort Linked List"
mathjax: true
toc: true
author_profile: true
---

# [Problem Statement](https://leetcode.com/problems/sort-list/)
Given the head of a linked list, return the list after sorting it in ascending order.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sort_linked_list1.jpg" alt="linked list number 1">

> Input: head = [4,2,1,3]<br />
Output: [1,2,3,4]


<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sort_linked_list2.jpg" alt="linked list number 2">

>Input: head = [-1,5,3,4,0]<br />
Output: [-1,0,3,4,5]

## Brute Force
The simple brute force approach for the given problem is:

1. Traverse through the linked list and add the elements to an ordinary list/array.
2. Sort the ordinary list in ascending order.
3. Create a dummy node with value=0 and elements next to it as the sorted list.
4. Return (dummy node).next

For Brute ForceThe Complexity is O(NlogN) and Space Complexity is O(N)

[TOP](#){: .btn .btn--danger}

## Merge Sort
We will solve this using Merge Sort with Top Down approach in Recursion. So Time Complexity will O(NlogN) and Space Complexity will be O(N)
General Algorithm to sort using Merge Sort is -
1. Split the list into two parts.
2. Compare the elements once we reach the Base Case.
3. Merge the list with the sorted values.

> The only difference for us will be in this for problem we will be applying Merge Sort on a Linked List.

Now, before we actually solve the proble. Let's look at the code of Merge Sort for a python list.

**PYTHON CODE FOR MERGE SORT**
```python
def mergeSort(arr):
    #split list into two parts
    left = [:len(arr)//2]
    right = [len(arr)//2:]

    #Recursively split lists further
    mergeSort(left)
    mergeSort(right)

    #Compare and Sort
    i, j, k = 0, 0, 0

    while i<len(left) and j<len(right):
        if left[i] < right[j]:
            arr[k] = left[i]
            i+=1
            k+=1
        else:
            arr[k] = right[j]
            j+=1
            j+=1
    while i<len(left):
        arr[k] = left[i]
        i+=1
        k+=1

    while  j<len(right):
        arr[k] = right[j]
        j+=1
        k+=1

```
[TOP](#){: .btn .btn--danger}

## Solution
1. Check whether given linked list is empty or contains single element and if true, return same linked list.
2. Split the linked list into left and right using a helper function *getMid*
```python
left = head
right = self.getMid(head)
tmp = right.next
right.next = None
right = tmp
```
3. Recursively split the lefts and rights, till we reach base case and then finally sort and merge those split linked lists using helper function *merge*

4. *getMid* function uses two pointer technique of fast and slow pointers, where slow moves at 1x and fast moves at 2x speed. So when fast reaches end of list, slow reaches middle of list.
```python
slow = slow.next
fast = fast.next.next
```
5. In the final step, we simply compare left and right list values, to sort them.

[TOP](#){: .btn .btn--danger}

## Final Code
```python
Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
class Solution:
    def sortList(self, head):
        # if list if empty or catains just one element
        if not head or not head.next:
            return head
        
        #Split the list
        left = head
        right = self.getMid(head)
        tmp = right.next
        right.next = None
        right = tmp

        left = self.sortList(left)
        right = self.sortList(right)

        return self.merge(left,right)


    def getMid(self,head):
        slow = head
        fast = head.next

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow

    def merge(self, left, right):
        tail = dummy = ListNode()

        while left and right:
            if left.val<right.val:
                tail.next = left
                left = left.next
            else:
                tail.next = right
                right = right.next

            tail = tail.next
        
        if left:
            tail.next = left
        
        if right:
            tail.next = right
        
        return dummy.next
```


[TOP](#){: .btn .btn--danger}

## Conclusion
The Time Complexity for this solution is O(N) and Space Complexity is O(N).

Now the follow up on the Leetcode site is to solve the same problem with Time Comlpexity O(N) and Space Complexity O(1).
To solve the problem with this condition, we need Bottom Up Approach and the code is very big for that, since we have to check lot of edge cases. I do plan to solve using that approach as well in future.


> Hope you all are able take away something from here. Please **share** the post and **subscribe** to the blog.
If you find any mistake in what I have written or error in the code please drop a mail, I will do the needful as required. Until next time!





## References 

- [Neetcode](https://www.youtube.com/c/NeetCode) YouTube channel

- [Leetcode](https://leetcode.com/)


[TOP](#){: .btn .btn--danger}