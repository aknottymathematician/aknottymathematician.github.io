---

title: "Simplify Path"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Simplify Path"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/simplify-path/)

Given a string path, which is an **absolute path** (starting with a slash **'/'**) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period **'.'** refers to the current directory, a double period **'..'** refers to the directory up a level, and any multiple consecutive slashes (i.e. **'//'**) are treated as a single slash **'/'**. For this problem, any other format of periods such as **'...'** are treated as file/directory names.

The canonical path should have the following format:

* The path starts with a single slash **'/'**.
* Any two directories are separated by a single slash **'/'**.
* The path does not end with a trailing **'/'**.
* The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period **'.'** or double period **'..'**)

*Return the simplified canonical path.*

> **Example 1:** <br />
*Input:* path = "/home/"<br />
*Output:* "/home"<br />
*Explanation:* Note that there is no trailing slash after the last directory name.<br />

> **Example 2:**
*Input:* path = "/../"<br />
*Output:* "/"<br />
*Explanation:* Going one level up from the root directory is a no-op, as the root level is the highest level you can go.<br />

> **Example 3:**
*Input:* path = "/home//foo/"<br />
*Output:* "/home/foo"<br />
*Explanation:* In the canonical path, multiple consecutive slashes are replaced by a single one.

**Constraints:**
* 1 <= path.length <= 3000
* path consists of English letters, digits, period '.', slash '/' or '_'.
* path is a valid absolute Unix path.


## Approach
As per the constraints, the best way to solve the problem is by using **Stacks**. Here's why,<br />
Input - /a/b/c/../..

We add the directory names according to the rules in a stack

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/simplify_path_step1.png" alt="Step I">

After adding b and c to the stack, we come across, **..** which means go back to previous directory

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/simplify_path_step2.png" alt="Step II">

So we remove the directory names by using **pop()** function on stack, which removes the last element added in the stack.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/simplify_path_step3.png" alt="Step III">


## Solution
```python
def simplifyPath(path):
    stack = []
    cur = ""

    #reason for adding adding / in for loop is to 
    #take care of edge case where input does not end with /
    for p in path + "/":
        if p == "/":
            if cur == "..":
                if stack: stack.pop()
            else:
                stack.append(cur)
            cur = ""
        else:
            cur+=p
    return "/" + "/".join(stack)
```

## Conclusion
Time and Space Complexity both are O(N) where N is length of the string.<br />
Reason for that is there is one pass over the string and stack of maximum length N.

## Refrence
* [Simplify Paths - Neetcode](https://www.youtube.com/watch?v=qYlHrAKJfyA)