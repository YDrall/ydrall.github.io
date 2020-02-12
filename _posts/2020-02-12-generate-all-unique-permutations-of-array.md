---
layout: post
title: Generate all unique permuations of an array.
---

Given an array of integers print all unique permutation of array.
-------------
Input:

`[1, 2, 3]`

Output:

```
[1]
[2]
[3]
[1, 2]
[1, 3]
[2, 3]
[1, 2, 3]
```
I always had problems in understanding the algorithms of generating all permutation of array. So lets try to solve by dividing the problem into smaller problem sets.
Taking [1, 2, 3] as an input, we can see that permutation has unique set of outcome of sizes 1, 2 and 3., means from 1 to n.

Now lets write code to generate all permutation of size 1. It can be easily done by iterating over array and printing each single value of array.

```python
for i in range(0, len(arr)):
    print(arr[i])
```

We have successfully generated all unique permutation of size 1, Now we will generate unique permutation of size 2. Simple and straight forward approach is to use two pointers to track the first and second index of array we are using.

```python
for i in range(0, len(arr)):
    for j in range(i+1, len(arr)):
        print(arr[i], arr[j])

```

Similarly, we can generate unique permutations of size 3:

```python
for i in range(0, len(arr)):
    for j in range(i+1, len(arr)):
        for k in range(j+1, len(arr)):
            print(arr[i], arr[j], arr[k])

```
And what if we want to print all permutations at once? Well it can be done as follows: 

```python
for i in range(0, len(arr)):
    print(arr[i])    
    for j in range(i+1, len(arr)):
        print(arr[i], arr[j])
        for k in range(j+1, len(arr)):
            print(arr[i], arr[j], arr[k])

```

We can use same approach to generate permutations of 4, 5 ...n, but it will be require adding more loops to the code. But we can avoid it if we try to see the pattern in this approach. If you look carefully, the algorithm is just using the index of last pointer, increments it by one and iterates upto the length of arr, then repeat the same until the final pointer reaches at the end of arr. So we simply need to store this pointer in a queue.

The final approach I used is:
- Initialize a queue and insert all the indexes of array [[0], [1], [2], …, [n]]
- Pop the first index in array, print all the values on the indexes
- Iterate from last index in popped item + 1 to size of array
- Next indexes will be popped item + [current iteration index].
- Start from 2 again if queue is not empty.

Working code is:

```python
from collections import deque

qu = deque([[a] for a in range(len(arr))])
while qu:
    q = qu.popleft()
    print([arr[i] for i in q])
    for j in range(q[-1]+1, len(arr)):
        qu.append(q + [j])

```

