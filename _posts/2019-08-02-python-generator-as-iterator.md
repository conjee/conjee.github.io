---
layout: post
title: "Python Generator as Iterator"
categories: programming
---

## TL;DR

You can define the `__iter__` method as a *generator function* to avoid the boilerplate code of defining an *iterator* class:

{% highlight python %}
class RepeatedOneTwoThree:
    def __init__(self, times):
        self._times = times

    def __iter__(self):
        for _ in range(self._times):
            yield 1
            yield 2
            yield 3
{% endhighlight %}

```
>>> rott = RepeatedOneTwoThree(2)
>>> list(rott)
[1, 2, 3, 1, 2, 3]
```

## Background Problem

Recently, I came across a problem where I need to visit elements in several sorted linked lists in order.

A linked list is defined to be either a `None` or a `Node`:

{% highlight python %}
class Node:
    def __init__(self, x, next_=None):
        self.x = x
        self.next_ = next_
{% endhighlight %}

Examples:

`None` | `None` (an empty linked list)
`Node(1)` | `1` -> `None`
`Node(1, Node(2, Node(3)))` | `1` -> `2` -> `3` -> `None`

Given:

`2` -> `3` -> `8` -> `None`

`1` -> `4` -> `5` -> `None`

`2` -> `6` -> `None`

I want to visit, in order, the elements: 1, 2, 2, 3, 4, 5, 6, 8.

The algorithm is like a generalized version of the merge step in a merge sort; it is provided in Python's standard library: [heapq.merge](https://docs.python.org/3/library/heapq.html?highlight=heapq#heapq.merge). This function takes several *iterable*s as inputs and returns an *iterator* over the sorted elements. Now, the question becomes how to turn linked lists we defined previously into *iterable*s.

Let's first wrap a linked list in a `LinkedList` class that provides utility methods:

{% highlight python %}
class LinkedList:
    def __init__(self, *xs):
        self._head = None
        for x in reversed(xs):
            self._head = Node(x, self._head)
    
    def __str__(self):
        s = ''
        t = self._head
        while t is not None:
            s += f'{t.x} -> '
            t = t.next_
        else:
            s += 'None'
        return s
{% endhighlight %}

We can now create and view linked lists easily:

```
>>> xs = LinkedList(2, 3, 8)
>>> ys = LinkedList(1, 4, 5)
>>> zs = LinkedList(2, 6)
>>> print(xs)
2 -> 3 -> 8 -> None
```

## What Makes a Python Object Iterable?

A Python object is said to be *iterable* if the built-in function [`iter`](https://docs.python.org/3/library/functions.html#iter) returns an *iterator* on it. An *iterator* should have a `__next__` method that returns the next element every time it's called or raise a `StopIteration` exception if it exhausts all elements.

For a user defined class to be *iterable*, defining an `__iter__` method that returns an *iterator* is __sufficient__.

An *iterator* should also have an `__iter__` method that usually returns `self` so that the *iterator* itself is *iterable*. 🤔

## Implementing the Iterable Protocol

We'll define an `__iter__` method to make our `LinkedList` class iterable. For comparison, I'll show how that can be done using both a traditional way that defines an *iterator* class and a convenient way that uses a *generator function*.

### A Traditional Way

{% highlight python %}
class LinkedList:
    def __init__(self, *xs):
        self._head = None
        for x in reversed(xs):
            self._head = Node(x, self._head)

    class Iterator:
        def __init__(self, head):
            self._head = head

        def __iter__(self):
            return self

        def __next__(self):
            if self._head is None:
                raise StopIteration
            x = self._head.x
            self._head = self._head.next_
            return x

    def __iter__(self):
        return self.Iterator(self._head)

    def __str__(self):
        return ' -> '.join([str(x) for x in self] + ['None'])
{% endhighlight %}

We defined a `LinkedList.Iterator` class and made the `__iter__` method return a new instance of it.

The `__str__` method was modified to take advantage of the new *iterable* property of our `LinkedList`.

### Using a Generator Function

{% highlight python %}
class LinkedList:
    def __init__(self, *xs):
        self._head = None
        for x in reversed(xs):
            self._head = Node(x, self._head)

    def __iter__(self):
        p = self._head
        while p is not None:
            yield p.x
            p = p.next_

    def __str__(self):
        return ' -> '.join([str(x) for x in self] + ['None'])
{% endhighlight %}

That's it! 😀 We saved a lot of boilerplate code by implementing the `__iter__` method as a *generator function*.

Well, how does that work? Despite the name *generator function* and the keyword `def`, we shouldn't interpret a *generator function* in the same way for a normal function. We were, instead, instructing Python to generate 🙃 the definition for a *generator* factory function named `__iter__`. When `__iter__` is called, it returns a new *generator* object which produces exactly the objects we `yield`. Because *generator* objects automatically implement the *iterator* protocol, they can be used as *iterator*s.

## Back to the Problem

```
>>> xs = LinkedList(2, 3, 8)
... ys = LinkedList(1, 4, 5)
... zs = LinkedList(2, 6)
... 
... import heapq
... print(', '.join(str(x) for x in heapq.merge(xs, ys, zs)))
1, 2, 2, 3, 4, 5, 6, 8
```

For simplicity, I concatenated sorted numbers into a string and printed them out. However, it's worth noting that we could consume sorted elements on the fly and pay for only constant-ish additional space because `heapq.merge` returns an *iterator* and doesn't make a copy of elements.

## Endnote

There're few good reasons to implement linked lists in Python - probably [`collections.deque`](https://docs.python.org/3/library/collections.html#deque-objects) is all you need. The takeaway here is the convenient way of implementing the *iterable* protocol by defining `__iter__` as a *generator function*.
