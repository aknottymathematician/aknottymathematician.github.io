---

title: "Average of Levels in Binary Tree"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Average of Levels in Binary Tree"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement] (https://leetcode.com/problems/average-of-levels-in-binary-tree/)

Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within 10-5 of the actual answer will be accepted.

> **Example 1:** <br />
*Input:* root = [3,9,20,null,null,15,7]<br />
*Output:* [3.00000,14.50000,11.00000]<br />

> **Example 2:**
*Input:* root = [3,9,20,15,7]<br />
*Output:* [3.00000,14.50000,11.00000]<br />

**Constraints:**
The number of nodes in the tree is in the range [1, 10<sup>4<sup/>].
-2<sup>31<sup/> <= Node.val <= 2<sup>31<sup/> - 1


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

        result.append(sum(level)/len(level))
    return result

```

## Refrence
* [FlyKiller](https://flykiller.github.io/binarysearch/0070.html)