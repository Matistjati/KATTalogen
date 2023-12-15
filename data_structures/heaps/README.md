# Heaps/Priority queues

Heaps is a data structure that can always track the largest element in a set of elements, while adding and removing the largest element from this set.

For example if a set of items are $[2,19,4,10]$, then the we can always know that the largest element is $19$ in this case.

With heaps you can do the following:

- Add any element in $O(\log n)$
- Remove the largest element in $O(\log n)$.


## Heaps in Python
Python has a built-in library for Heaps/Priority queues. Simply run ```import heapq``` and use the functions

- ```heapq.heapify(list)``` to make a list into a heap.
- ```heapq.heappop(list)``` to pop the smallest element.
- ```heapq.heappush(list)``` to add an element to the heap.

Read more about it here:
 https://docs.python.org/3/library/heapq.html


## Problems: TODO (write more about this later)


https://open.kattis.com/problems/igra

https://open.kattis.com/problems/segmentovervakning