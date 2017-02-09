---
layout: post
title:  "Understanding Python Built-in Functions: zip()"
date:   2017-02-08 03:30:00
categories: main
---

## Python Built-in Functions
Welcome to the first post of the ***Python Built-in Functions*** series. This series is my attempt to understand Python Built-in functions better, and explain them more comprehensively. Let's get started. 

## [zip()](https://docs.python.org/3/library/functions.html#zip)

**Arguments**: zip() takes one or more sequences or iterables.

**Return**: zip() returns an **iterator of tuples**, where *the i-th tuple contains the i-th element from each of the argument sequences or iterables*.

For example:
```python
>>> x = [1, 2, 3]
>>> y = [4, 5, 6]
>>> zipped = zip(x, y)  # zipped is an iterator
>>> list[zipped]        # We make a list using zipped iterator
[(1, 4), (2, 5), (3, 6)]
```

Keep in mind that if you feed in sequences of **unequal length** into zip function, the iterator stops when the shortest input iterable is exhausted.

For example:
```python
>>> a = [3, 4, 5, 6, 7]
>>> b = [0, 1]
>>> zipped = zip(a, b)
>>> list[zipped]
[(3, 0), (4, 1)]
```

## Usage: Transposing a matrix

Zip can be used to transpose a matrix (i.e to make a new matrix whose rows are the columns of the original). We will represent a matrix as **a list of lists** in python. For example, here is a 2x3 matrix.

```python
matrix = [[1, 2, 3], [4, 5, 6]]

# So, here is our original matrix.
[ [1, 2, 3], 
  [4, 5, 6] ]

# We want to transpose it to:
[ [1, 4], 
  [2, 5],
  [3, 6] ]
```


How do we use the zip function to do this? 
```python
>>> matrix = [[1, 2, 3], [4, 5, 6]]
>>> transposed = list(zip(*matrix))
>>> transposed
[ (1, 4), (2, 5), (3, 6) ]
```

Isn't this one-liner transpose function cool? It works for any *n by m* matrix.

*Side-note*: Keep in mind that our transposed matrix becomes **a list of tuples**, instead of our original format. This is because zip() returns an iterator of tuples. If we want the result to be **a list of lists**, we can use **list comprehension**, which is a topic for another day. In short, we can do:

```python
>>> matrix = [[1, 2, 3], [4, 5, 6]]
>>> transposed = [list(tup) for tup in zip(*matrix)]
>>> transposed
[ [1, 4], [2, 5], [3, 6] ]
```

Quick Explanation: In short we are defining a new list like this: [*list definition*]. ```zip(*matrix)``` returns an iterator of tuples, and we turn each tuple into a list with ```list(tup)```, resulting in a list of lists.

## zip(*matrix) and starred(\*) operator

Let's take a closer look at ```list(zip(*matrix))```. Shall we?

```list()``` is simple enough. The function takes an iterable and returns a list. 

What is ```zip(*matrix)``` doing? To understand this, we need to take a look at what the starred operator (\*) in python does. Here is an excerpt from the [documentation](https://docs.python.org/3/reference/expressions.html#calls).

> If the syntax *expression appears in the function call, expression must evaluate to an iterable. Elements from these iterables are treated as if they were additional positional arguments. For the call f(x1, x2, *y, x3, x4), if y evaluates to a sequence y1, ..., yM, this is equivalent to a call with M+4 positional arguments x1, x2, y1, ..., yM, x3, x4.

\* is used to unpack an iterable in Python 3. To illustrate this in a simple example.
```python
>>> numbers = [1, 2, 3, 4, 5]
>>> foo(*numbers)                 # This call is the same as the following.
>>> foo(1, 2, 3, 4, 5) 
```
Remember that our matrix is a list of lists? ```*matrix``` unpack our matrix into lists (where each list represent a row), and feed them into the ```zip()``` function which does, you know ... zip things, resulting in a transposed matrix. So, ```zip(*matrix)``` has the same effect as ```zip([1, 2, 3], [4, 5, 6])```

That's all for today. I will add more content soon. Let me know if there is something I can correct or add to this post.

## Notes
* This post assumes Python version of 3.6.0.
