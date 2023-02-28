# Algorithms with explained solutions 

Notes
## Linked List

q: Why use linked list instead of array list? 
a: Imagine a if you have [a,b,c,d] in both structures. If you need to add an value "x" where b is, in array you need to shift all elements(assuming you have the space to the right) and then insert x. Linked list you traverse the list and point b node to x then x to c. Without carrying how many more elements are after.  
Resulting in O(1) time for linked list, while array will be O(n)

## Code Cheatsheet 


### Heaps

By default, when we refer to heap, most implementations are min-heaps. This means the first element is always the smallest element.

In Python, you can use the following functions to interact with a heap:
```python
heap = [] #to initialize a heap, it is just a list

heappush(heap, 3) # to add an element to the heap, we can use heappush
#heap = [3] 

heappush(heap, 5)
#heap = [3, 5] , the heap always keeps the smallest element in front!

smallest_element_from_heap = heappop(heap) #we can remove the first element from heap with heappop
#heap = [5] , 3 is removed
#smallest_element_from_heap = 3  #after heappop, it is stored in the variable
```

That's it! These are the operations you need for using heap in LeetCode.

There is one more trick to learn for usi ng heap. How do we tweak the heap to make it a max-heap?

```python
max_heap = []

#we want to store 10, but change it to -10 for max-heap
heappush(max_heap, -10)
#max_heap = [-10]


#we want to store 7, but change it to -7 for max-heap
heappush(max_heap, -7)
#max_heap = [-10, -7]

max_element_from_heap = -1 * heappop(heap)
#heap = [-7], -10 is removed
#max_element_from_heap = 10, we have retrieved the largest element from the heap
```