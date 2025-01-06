# Heaps/Priority queues

Heaps are a data structure that can always track the largest element in a set of elements, while adding and removing the largest element from this set.

For example if a set of items are $[2,19,4,10]$, then it will report that the largest element is $19$ in this case, and will update accordingly if we add/remove numbers.

With heaps you can do the following:

- Add any element in $O(\log n)$
- Remove the largest element in $O(\log n)$.
- Get the largest item

## Heaps in Python
Python has a built-in library for Heaps/Priority queues. Simply run ```import heapq``` and use the functions

- ```heapq.heapify(list)``` to make a list into a heap.
- ```heapq.heappop(list)``` to pop the smallest element in the heap.
- ```heapq.heappush(list, x)``` to add an element x to the heap.

Read more about it here:
 https://docs.python.org/3/library/heapq.html


## Problems: TODO (write more about this later)


https://open.kattis.com/problems/igra

https://open.kattis.com/problems/segmentovervakning
