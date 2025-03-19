# Priority queue and adaptable priority queue

## Operations

### Priority queue

| Operation           | Description                                                                  |
| ------------------------ | -------------------------------------------------------------------------------- |
| `func top() -> E`        | Returns the element with the top priority without removing it.                   |
| `func add(element: E)`   | Adds an element to the priority queue.                                           |
| `func remove_top() -> E` | Removes and returns the element with the highest priority in the priority queue. |

### Adaptable priority queue

| Extended operation           | Description                                             |
| -------------------------------- | ------------------------------------------------------------ |
| `func remove(e: E) -> E`         | Removes and returns the element `e` from the priority queue. |
| `func replace_key(e: E, k: K)`   | Replaces the key of existing element `e` with `k`.           |
| `func replace_value(e: E, v: V)` | Replaces the value of existing element `e` with `v`.         |

## Binary heap

### Definition

A binary heap is a binary tree with the following two properties:
1. Complete property: All the levels of a heap are completely filled, except (possibly) for the last level. The filled items in the last level are left-justified.
2. Heap-order property: For any node $i$, the key of the key of parent of $i$ is larger than or equal to key of $i$ if it's a max heap, and the key of parent of $i$ is less than or equal to key of $i$ if it's a min heap.

<img src="images/Pasted%20image%2020250313094732.png" width="300">

### Storing heaps

Heaps are typically stored in dynamic arrays, thanks to *Eytzinger*'s layout, where:
- the root node is at index $1$
- the left child of node $i$ is node $2i$
- the right child of node $i$ is node $2i + 1$
- the parent of node $i$ is node $\lfloor \frac{i}{2} \rfloor$

<img src="images/Pasted%20image%2020250305000853.png" width="500">

> [!note]
> Index $0$ is not used.

### Complexities

#### Worst case time complexity

| **Operation** | **Worst case time complexity** |
| ------------- | ------------------------------ |
| Build heap    | $O(n)$                         |
| Lookup        | $O(1)$                         |
| Insertion     | $O(\log n)$                    |
| Deletion      | $O(\log n)$                    |

#### Worst case space complexity

$O(n)$

### Node sifting mechanisms

#### Heapify up/sift up/bubble up 

For some node, we repeatedly sift the node up if the node's key is less than its parent's key (min-heap) or if the node's key is greater than its parent's key (max-heap) by swapping positions with its parent.

<img src="images/Pasted%20image%2020250313094956.png" width="200">

#### Heapify down/sift down/bubble down

For some node, we repeatedly sift the node down when its key is greater than one of its children's key by swapping it with the smallest children (min-heap) or when its key is less than one of its children's key by swapping it with the largest children (max-heap).

<img src="images/Pasted%20image%2020250313095008.png" width="200">

### Building a heap from initial elements

To build a heap from initial elements of a list in $O(n)$ worst case, we build in a bottom-up manner as follows:
1. Copy over all elements in the original list into the backing array
2. Beginning at the parent of the last element in the backing array, and repeatedly call the heapify down method

### Search

Typically, binary heaps are used as containers for priority queues. This means that we'll typically search for the topmost element in the heap i.e. the root node. As such, we simply return the element at index of the root node: index $1$. For any other elements, we have to perform a linear search.

### Insertion

1. Add an element as the rightmost leaf of the heap (i.e. the last element in the backing array)
2. Sift up the node containing the element to correct its position within the tree

### Deletion

1. Set the root node's key to be the same key of the last node in the heap
2. Remove the last node in the heap now that we've placed its key in the root node
3. Sift down the root node to its correct position

