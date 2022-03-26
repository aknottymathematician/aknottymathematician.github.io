---

title: "Binary Tree Level Order Traversal I & II"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Binary Tree Level Order Traversal I & II"
mathjax: true
toc: true
author_profile: true
---

## Problem Statement [I](https://leetcode.com/problems/binary-tree-level-order-traversal/) and [II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

**Problem I** Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).
**Problem II** Given the root of a binary tree, return the reverse level order traversal of its nodes' values. (i.e., from left to right, level by level).

> **Example 1:** <br />
*Input:* root = [3,9,20,null,null,15,7]<br />
*Output:* [[3],[9,20],[15,7]]<br />

> **Example 2:**
*Input:* root = [1]<br />
*Output:* [[1]]<br />

> **Example 2:**
*Input:* root = []<br />
*Output:* []<br />

**Constraints:**
* The number of nodes in the tree is in the range [0, 2000].
* -1000 <= Node.val <= 1000


## Approach

We use BFS traversal.

What is level in our binary tree? It is set of nodes, for which distance between root and these nodes are constant. And if we talk about distances, it can be a good idea to use bfs.

We put our root into queue, now we have level 0 in our queue.
On each step extract all nodes from queue and put their children to to opposite end of queue. In this way we will have full level in the end of each step and our queue will be filled with nodes from the next level.
In the end we just return result.

**Complexity**: Time complexity is O(n), space complexity is O(n).


## Solution for Problem I
```python

def levelOrder(root):
    queue = deque([root])
    result = []

    while queue:
        level = []
        for i in range(len(queue)):
            curNode = queue.popleft()
            level.append(curNode.val)

            if curNode.left: queue.append(curNode.left)
            if curNode.right: queue.append(curNode.right)

        result.append(level)
    return result

```

## Solution for Problem II
```python

def levelOrder(root):
    queue = deque([root])
    result = []

    while queue:
        level = []
        for i in range(len(queue)):
            curNode = queue.popleft()
            level.append(curNode.val)

            if curNode.left: queue.append(curNode.left)
            if curNode.right: queue.append(curNode.right)

        result.append(level)
    return result[::-1]

```


## Refrence
* [FlyKiller](https://flykiller.github.io/binarysearch/0070.html)