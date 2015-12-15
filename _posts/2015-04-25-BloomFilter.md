---
layout: minimal_post
title: Bloom Filter
comments: true
<<<<<<< Updated upstream
introduction: BloomFilter
published: true
---


###Introduction
=======
introduction: Bloom Filter
---

This blog tries to summarize the Bloom Filter, and answer the below three questions. **_What is Bloom Filter?_** **_How to build a Bloom Filter?_** **_How to realize Bloom Filter algorithm in Java?_**
>>>>>>> Stashed changes

### 1. What is Bloom Filter?
The Bloom filter is a **probabilistic set data structure**, proposed by Burton Howard Bloom in 1970[1]. In general, The Bloom Filter algroithm is used for testing whether an element is a member of one set with a fewer storage space than general algorithms. For example, considering a scenerio of detecting email spam, the user wants to detect and filter the spam automatically. The general algorithm is simple. First, we can store plenty of spam addresses. Then, when receving an email, the algorithm will compare the coming email address and spam addresses separatly. If matching any of the spam addresses, the email will be recognized as a spam and be filtered, otherwise, it can be saved. We can figure out that a large number of storage space is necessary for plenty of spam addresses, if we want to guarantee a good detection rate. Actually, the spam detection problem can be simplified as testing whether an element is in a set. In this scenerio, spam addresses can be seen as one set, and a receving email address is a member. So, we can use Bloom Filter to solve this kind of problem according to its defination. Comparing with general algorithms, while using Bloom Filter, we can effectivly reduce the storage space, just with a low false positive detection rate. In next section **_How to build a Bloom Filter?_**, I will discuss about the Bloom Filter algorithm.Besides spam detection, the Bloom Filter can be used for other purposes, such as detecting repeated URL when spidering websites[2], data aggregation[3], 

### 2. How to build a Bloom Filter?

There are basic two kinds of Bloom Filter, the regular one and counting one. These two algorithms will be introduced separatly.

#### 2.1 Regular Bloom Filter

The storage of regular Bloom Filter can be seen as a vector. As shown in Fig 1, every element in this vector can store 1 bits, which means the value are only be 0 or 1.

[Fig1]

_(1) Setup_  
The set's length is $$n$$, and the vector's length is $m$, and different $$k$$ [hash functions]() has been chosen to hash every elements to set separatly. The hash function can map input to one of position in the vector and this position will be set to 1.  
_(2) Search_  
There comes a new data, and we should test whether it is in this set. We use different $$k$$ hash fucntions to hash this data, and map them to the positions of vector. If the positions' values are all 1, then we believe that the data is in this set, otherwise, we think it's not.  

The results of search obviously have [false positive](). Maybe the data is not in this set, but the mapping positions in vector are all 1, because of other data's effection. Therefore, the false positive rate should be analyzed to help to choose better parameters and make false positive rate lower.  

Assuming that hash functions are all great hash functions, and they can map the input data to vector with average possibility. The possibility that one of positions in the vector isn't set to 1 after $$k$$ hash functions for one input data is,

$$ 
P_1=\left(1-\frac{1}{m}\right)^k.
$$

after we insert $n$ data to the vector, the possibility that this position still isn't be set is,

$$
P_2=\left(1-\frac{1}{m}\right)^{kn}
$$

Therefore, the possibility that the position is set is,

$$
P_3=1-P_2=1-\left(1-\frac{1}{m}\right)^{kn}
$$

According to the above equation, we get the false positive rate,

$$
P=P_3^k=\left(1-\left(1-\frac{1}{m}\right)^{kn}\right)^k
$$


#### 2.2 Counting Bloom Filter

### 3. How to realize Bloom Filter algorithm in Java?

#### 3.1 Regular Bloom Filter

#### 3.2 Counting Bloom Filter

### Reference






<<<<<<< Updated upstream
###Conclusion
=======

>>>>>>> Stashed changes
