---

title: "Shortest Path Visiting All Nodes"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Shortest Path Visiting All Nodes"
mathjax: true
toc: true
author_profile: true
---

# [Problem Statement](https://leetcode.com/problems/shortest-path-visiting-all-nodes/)
You have an undirected, connected graph of n nodes labeled from 0 to n - 1. You are given an array graph where graph[i] is a list of all the nodes connected with node i by an edge.

Return the length of the shortest path that visits every node. You may start and stop at any node, you may revisit nodes multiple times, and you may reuse edges.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/shortest-path1-graph.jpg" alt="graph number 1">

>Input: graph = [[1,2,3],[0],[0],[0]]<br />
Output: 4 <br />
Explanation: One possible path is [1,0,2,0,3]


<img src="{{ site.url }}{{ site.baseurl }}/assets/images/shortest-path2-graph.jpg" alt="graph number 2">

>Input: graph = [[1],[0,2,4],[1,3,4],[2],[1,2]]<br />
Output: 4<br />
Explanation: One possible path is [0,1,4,2,3]

**Constraints:**

1. n == graph.length
2. 1 <= n <= 12
3. 0 <= graph[i].length < n
4. graph[i] does not contain i.
5. If graph[a] contains b, then graph[b] contains a.
6. The input graph is always connected.



## Breadth First Search
The basic idea behind the problem is to find a shortest path connecting all the nodes. In general whenever we have to find the shortest path in a given undirected graph, we can simply use **Breadth First Search(BFS)**.

Let us look at BFS algorithm,
```python
import collections

def bfs(graph, root_node):
    #add visited nodes to avoid duplicate values i.e. revisiting the node
    visited = set()
    #initialize a queue DS with root node
    queue = collection.deque([root_node])

    while queue:
        #until queue is not empty traverse through the graph 
        # while deleting visited nodes from queue and 
        # adding them in visited set
        vertex = queue.popleft()
        visited.add(vertex)

        for i in graph[vertex]:
            if not i in visited:
                queue.append(i)
    return visited
```

Now, BFS algorithm is designed in such a way that we visit each node only once. But in the problem it is given that we can revisit a node multiple times, which creates a slight setback since we cannot use BFS directly here, since if we do we run into the risk of getting into infinite loops. So the way around this issue is to make sure that we track all the visited nodes. And we do that by using **Bit Mask**.

>**NOTE -** To be able to successfully traverse the shortest path, we will be using five parameters,<br />
**curState** - gives bitmask of a current node, i.e. this will tell whether we have traversed this path or not. (1 if visited and 0 if not visited).<br />
**endState** - It tells us what is our final state, so that we keep comparing our current state and know when we have traversed shortest path <br />
**path_len** - This will tell the length traversed in the path.<br />
**queue** - we add every node to it along with it's state, since we consider every node as a starting potential node.<br />
**Set DS *visited*** - It tells us which path we have already visited. It does not allow us to travel the repeative paths.

If the same node was visited again with same visitedNodeBit, it means this node can be skipped, For example: 1->0->1->0.  First 1 we have {1, 10}, then we have {0, 11}, then we will have {1, 11}. Lastly, we have {0, 11} which is a state we already had before. So we don't visit this again.


[TOP](#){: .btn .btn--danger}

## BFS with BitMasking

Before we dive into the actual code let us look at the algorithm,
```
Setup parameters
    1. endState = (1 << n) - 1 #(a<<b) = a * (2^b)
    2. Mak of a node represented by 1 << node, gives the path we have traversed before reaching that node.
    3. So we make queue = [(node, 1 << node) for node in range(n)]
    4. visited = set(queue) => every visited state would be (node, mask)
    5. path_len = 0
BFS Queue
    1. Loop through queue.
    2. For every node in queue check if it's curState matches endState.
    3. If that node and state are visited do nothing else add to the set.
    4. Add all neighbouring nodes of the current node to the queue and update the state.

```

## Final Code


```python
import collections

def shortestPathLength(graph):
    n = len(graph)
    endState = (1<<n)-1

    path_len = 0
    queue = collections.deque() # add tuple (node, state)
    visited = set()

    #Since every node is a possible starting point, add it to queue
    for i in range(n):
        queue.append((i, 1<<i))
    
    # Now it's a simple BFS algorithm
    while queue:
        for i in range(len(queue)):
            node, curState = queue.popleft()

            if curState == endState:
                return path_len

            #For example: 1->0->1->0.  First 1 we have {1, 10}, then we have {0, 11}, then we will have {1, 11}. Lastly, we have {0, 11} which is a state we already had before. So we don't visit this again.
            if (node, curState) in visited:
                continue
            
            visited.add((node, curState))
            for next_node in graph[node]:
                queue.append((next_node, curState | 1<<next_node))
        path_len+=1
    
    return -1


```
[TOP](#){: .btn .btn--danger}

## Important Note
Before we conclude today's discussion, I would like to highlight couple of points, 

1. In the last part of the code where we append next node to the queue, we have used **OR** operator on integer. Here's an example to highlight how that works.

```python

a = 2
b = 5
In binary form, a = 010 and b = 101
when we perform a | b,
a   0   1   0
b   1   0   1
--------------
a|b 1   1   1

Therefore, a|b = 7

```

2. Second point is about Bit Masking, even though it is an intuitive topic it will require a blog of it's own to understand properly. Will definitely cover that in future. But till then, you can refer to [this](https://www.youtube.com/watch?v=iQBxxTZDajU) amazing explanation by [Ayushi Sharma](https://www.youtube.com/channel/UCSnJKXPKhxS_tcaTcIZrPYg) to get a good understanding of the topic.

[TOP](#){: .btn .btn--danger}

## Conclusion
The Time Complexity for this solution is O(N<sup>2</sup>*2<sup>N</sup>) and Space Complexity is O((N*2<sup>N</sup>)).

**Explanation -**
1. Now, the time complexity depends on how many times while loop is running. 
2. So, if while loop will run until queue is not empty, how many nodes will be there in queue. 
3. That will be, N nodes and for those N nodes there can be 2^ N states for each node.
4. Now inside the while loop , we are traversing to each neighbour, in worst case, a node can have n-1 neighbors, so O(N) time for that, hence total time complexity is O(N*(2<sup>N</sup>) *N)
5. And the Space Complexity is storing 2^N states for N elements i.e. O(N*2<sup>N</sup>)


> Hope you all are able take away something from here. Please **share** the post and **subscribe** to the blog.
If you find any mistake in what I have written or error in the code please drop a mail, I will do the needful as required. Until next time!





## References 

- [Coding Decoded](https://www.youtube.com/watch?v=1XkMFNvkouo) 

- [William Fiset](https://www.youtube.com/watch?v=oDqjPvD54Ss)

- Leetcode Discussion


[TOP](#){: .btn .btn--danger}