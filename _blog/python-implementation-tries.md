---
title: "Tries"
header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Sort Linked List"
mathjax: true
toc: true
author_profile: true
---

## [Problem Statement](https://leetcode.com/problems/implement-trie-prefix-tree/)
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- Trie() Initializes the trie object.
- def insert(String word) Inserts the string word into the trie.
- def search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
- def startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.
 

**Example 1:**

> Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]<br />
*Output*<br />
[null, null, true, false, true, null, true]<br /><br />
*Explanation*<br />
Trie trie = new Trie();<br />
trie.insert("apple");<br />
trie.search("apple");   // return True<br />
trie.search("app");     // return False<br />
trie.startsWith("app"); // return True<br />
trie.insert("app");<br />
trie.search("app");     // return True<br />
 

**Constraints:**<br />
1 <= word.length, prefix.length <= 2000<br />
word and prefix consist only of lowercase English letters.<br />
At most 3 * 104 calls in total will be made to insert, search, and startsWith.


```python
class TrieNode:
    '''
    Not storing the node itself in the TrieNode class. Will be implicit from the HashMap.Example - children["a"] = TrieNode()
    '''
    def __init__(self):
        self.children = {}
        self.endOfWord = False # applicable for every node

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        '''
        Insert the word in the tree
        '''
        cur = self.root

        for w in word:
            if not w in cur.children():
                cur.children[w] = TrieNode()
            cur = cur.children[w]
        
        cur.endOfWord = True
    
    def search(self, word):
        cur = self.root

        for w in word:
            if not word in cur.children:
                return False
            cur = cur.children[w]
        return cur.endOfWord
    
    def startsWith(self, prefix):
        cur = self.root

        for p in prefix:
            if not p in cur.children:
                return False
            cur = cur.children[w]
        return True



```