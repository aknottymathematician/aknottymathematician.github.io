---

title: "Sort Linked List"
permalink: /sort-linked-list/
date: 2022-02-22
layout: single
classes: wide
comments: true
author_profile: false
related: true
share: true
read_time: true
tags:
    - DSA
    - Linked List
    - Sorting
    - Merge Sort

header:
  image: "/assets/images/DSA_Problems_Banner_22-Feb-2022.png"
  teaser: "/assets/images/DSA_Problems_Teaser_22-Feb-2022.png"
excerpt: "Sort Linked List"
mathjax: true
toc: true

---

# Problem Statement
Given the head of a linked list, return the list after sorting it in ascending order.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sort_linked_list1.png" alt="linked list number 1">

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/sort_linked_list2.png" alt="linked list number 2">

We will solve this using Merge Sort. So Time Complexity will O(NlogN) and Space Complexity will be O(N)
General Algorithm to sort using Merge Sort is -
1. Split the list into two parts.
2. Compare the elements once we reach the Base Case.
3. Merge the list with the sorted values.

> The only difference for us will be in this for problem we will be applying Merge Sort on a Linked List.


```
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
## Text data surrounds us!

Now, when we talk about conversation between humans, it has two aspects, the voice and the text. Natual language processing(NLP) focuses on the text part of the conversation. Somehow, this is one of the things that we never think about, the amount of text data around us. But with the growing presence of "intelligent machines" in our lives, it is imperative the we try and "teach" those machines our languages. Now machines, or to be more precise mathematical models which learn our languages, understand only only numerical values, so ideally our job comes down to converting text into numerical entities so that the models can find patterns. So without any further adieu let's see how to teach machines our languages.

[TOP](#){: .btn .btn--danger}

## Preprocessing the data
So before we actually run the NLP models, it is very important to process the corpus(text data) and make sure that it is clean and without any garbage. A clean corpus will allow a model to learn meaningful features and not overfit on irrelevant noise. 

A general checklist for preprocessing would be -

1. Remove all irrelevant characters such as any non alphanumeric characters, @ twitter mentions or URLs.

2. Tokenize your text by separating it into individual words called "unigrams" or into pairs of two words called "bi-grams" or into groups of n words known as "n-grams". 

3. Remove stop words, which is essentially a list of words which might occur many times in the corpus but aren't very important. Example - "am", "a", "the" etc.

4. Convert all characters to lowercase, in order to treat words such as “book”, “Book”, and “BOOK” the same.

5. Combining misspelled or alternately spelled words to a single representation (e.g. “cool”/”kewl”/”cooool”).

6. Stemming, an algorithm which chops off the suffix of the word to arrive at the root of it, for example - preprocessing will become preprocess after stemming.

7. Lemmatization, though similar to stemming is a more intelligent algorithm, for example - *better* would be reduced to bet or bett from **stemming** but would reduce to good from **lemmatization**

>**_NOTE_** It is important to realise that there is no one right answer when it comes to choosing between lemmatization and stemming. **It all depends on the data!**

[TOP](#){: .btn .btn--danger}

## Vectorization
Once we have split our text samples into n-grams, we need to turn these n-grams into numerical vectors that our machine learning models can process. Let us look at some of those processes starting with - 

### One Hot Encoding
In one hot encoding, we essentially represent each word as a vector of length N, where N is the total number of unique words available in the entire textual data. N is also called the vocabulary count. Each word’s one hot encoded vector is basically a binary vector with the value 1 being in a unique index for each word and the value 0 being in every other index of the vector. Let’s visualize this.
Suppose our data comprises of the following 2 sentences:
*All movies are not bad*
*Some movies are fun*
Here, the value of N is 7, because there are 5 unique words: ['all’, ‘movies’, ‘are’, ‘not’, 'bad', 'some', ‘fun’]. Now to represent each word, we will use a vector of length 7.




This is a simple and straightforward approach to convert all the words in a set of data into numbers and is one of the first methods implemented for this purpose, however this method has many issues.

Firstly, the size of each word’s one hot encoded vector will always be N, which is the size of the entire vocabulary. In the example it was 7 but in real life scenario the value of N can reach 10k or 100k or even millions depending on the corpus in context. This means we need a huge vector just to represent a single word, which can lead to excessive memory usage while representing text as vectors.

Secondly, the index which is assigned to each word does not hold any **semantic meaning**, it is merely an arbitrary vector assigned to it. When we consider the vectors for two words, we would ideally want the vectors of similar meaning to have similar vectors. Say, for example, what we would expect is, the vectors for “Man” and “Woman” are close to each other since the words share certain amount of similarity. However, with one hot encoded vectors, the vectors for “Man” and “Woman” are just as close to each other as “Man” and “Rocket”. Hence the neural network has to work really hard to understand each word since they are being treated as completely isolated entities.

### Bag-of-Words with TF-IDF

Now as we saw with one hot encoding there was one issue of excessive memory and other issue of lack of understanding of semantic meaning between the words. To deal with, especially the second issue we try bag of words approach.

Bag of Words is a representation model of document data, which simply counts how many times a word appears in a document. Bag-of-Words is commonly used in clustering, classification, and topic modeling by weighing special words and relevant terminologies. Below is a flow of Bag-of-Words transformation.

```python
#Sample Sentences
All movies are not bad. Some movies are fun
Tokenization - "All","movies","are","not","bad","some", "movies", "are","fun"
Creating word set - 
"All", "are", "bad", "movies", "not", "some","fun"
Generating a Bag-of-words.
{"All":1, "are":2, "bad":1, "movies":2, "not":1, "some":1,"fun":1}

```

The process is intuitively understandable. First step is tokenization, which transform sentence to tokens. Second is creating a list, which removes word duplication and make word set(which is called dictionary or vocabulary). Final step is counting occurrences of each words and make it Bag-of-Words model. As you can see, "are" and “movies” show 2 as they appears two times in sample sentences.



#### TF-IDF
TF-IDF stands for “Term Frequency — Inverse Document Frequency”.

**Term Frequency (TF)**\
The number of times a word appears in a document divded by the total number of words in the document. Every document has its own term frequency.

**Inverse Document Frequency (IDF)**\
The log of the number of documents divided by the number of documents that contain the word w. Inverse data frequency determines the weight of rare words across all documents in the corpus.

$$tfidf( t, d, D ) = tf( t, d ) \times idf( t, D )$$


>Where **t** denotes the **terms**; **d** denotes each **document**; **D** denotes the **collection of documents**.


Simply speaking TF-IDF ranks a word based on the number times it occurs in a sentence versus number of times it occurs in a document.

Thus by evaluating TF-IDF or a number of “the words used in a sentence vs words used in overall document”, we understand -

- how useful a word is to a sentence (which helps us understand the importance of a word in a sentence).

- how useful a word is to a document (which helps us understand the important words with more frequencies in a document).

- helps us ignore words that are misspelled

Consider a document where "movies" is misspelled as "mvies" -
In case of Bag-of-words, both "movies" and "mvies" would be treated as different words and given the same importance because their frequency is same. But in case of TD-IDF because of a score of IDF, this mistake is corrected because we know movies as a word is more important than mvies, so we treat it like a non useful word.

Now even though we have improved on our previous method, tf-idf still lacks the way to capture sematic meanings of the words.

[TOP](#){: .btn .btn--danger}


## Conclusion
All the methods that we saw are merely based on counting and though a bad way definitely doesn't help a ML model in understanding the nuances of the
words.
To improve on that we need to make use of word embeddings, which assign each word a vector and based on the "closeness" of those vectors model understands the patterns.


Hope you all are able take away something from here. Please **share** the post and **subscribe** to the blog.
If you find any mistake in what I have written or error in the code please drop a mail, I will do the needful as required. Until next time!



## References 

- [NLP by Sentdex](https://www.youtube.com/watch?v=FLZvOKSCkxY&list=PLQVvvaa0QuDf2JswnfiGkliBInZnIC4HL) YouTube channel by Harrison Kinsley

- [CS224N: Natural Language Processing with Deep Learning](https://www.youtube.com/playlist?list=PLoROMvodv4rOhcuXMZkNm7j3fVwBBY42z)


[TOP](#){: .btn .btn--danger}