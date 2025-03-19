# Ordered map and ordered set

## Operations

| **Extended operation**          | **Description**                                        |
| ------------------------------- | ------------------------------------------------------ |
| `func min() -> K`               | Returns the smallest key in the ordered map.           |
| `func max() -> K`               | Returns the largest key in the ordered map.            |
| `func successor(key: K) -> K`   | Finds the key that immediately follows the given key.  |
| `func predecessor(key: K) -> K` | Finds the key that immediately precedes the given key. |

## AVL tree

### Time complexity

| **Operation** | **Time complexity**    |
| ------------- | ---------------------- |
| Lookup        | Worst-case $O(n)$      |
| Insertion     | Worst-case $O(\log n)$ |
| Deletion      | Worst-case $O(\log n)$ |

## Red-black tree

### Overview

#### black height

TO DO

#### properties

TO DO

> [!note]
> When calculating the black height, remember that there are implicit `nil` leaf nodes which are always coloured black.

### Time complexity

| **Operation** | **Time complexity**    |
| ------------- | ---------------------- |
| Lookup        | Worst-case $O(n)$      |
| Insertion     | Worst-case $O(\log n)$ |
| Deletion      | Worst-case $O(\log n)$ |
### Search
### Insertion

Suppose our inserted node is called `z`, and its uncle node is called `y`. We'll call `z`'s parent and grandparent as is.

#### Case 0: node `z` is the root of the entire tree, and is red

Re-colour `z` to black

<img src="images/Pasted%20image%2020250208104340.png" width="200">

#### Case 1: node `y` is red

1. Re-colour `z`'s parent and `y` to black, and re-colour `z`'s grandparent to black
2. Set the current `z`'s grandparent as the new `z` 

<img src="images/Pasted%20image%2020250208105256.png" width="600">

#### Case 2: node `y` is black and there’s a triangle with `z`, `z`’s parent, and `z`’s grandparent

1. Set `z` to be `z`'s parent
2. Rotate `z`'s parent in the opposite direction of `z` such that `z` takes the place of its parent
3. Go to case 3

<img src="images/Pasted%20image%2020250223055050.png" width="600">

#### Case 3:  node `y` is black and there’s a line with  `z`, `z`’s parent, and `z`’s grandparent

1. Rotate `z`'s grandparent in the opposite direction of `z`
2. Re-color `z`'s parent and `z`'s old grandparent

<img src="images/Pasted%20image%2020250223060410.png" width="1000">

### Deletion

TO DO

## In-memory B-Tree

### Overview

According to *Introduction to Algorithms*, a B-Tree is a rooted tree with the following properties:

#### Node

For some node `x`, it has the following attributes:
- `key_count: Int`, the number of keys currently stored in node `x`
- `keys: Array[K]`, an array of keys of type `K` sorted in increasing order.
- `leaf: Bool`, a boolean value that is `True` if `x` is a leaf, and `False` if `x` is an internal node.
- `children: Array[BTreeNode]`, an array of `x`'s child nodes

#### Node and children count

$$
\text{For some node with } |keys|, \text{ then } |children| = |keys| + 1
$$

#### Keys as separators

The keys in the node separate the ranges of keys stored in its subtrees.

#### Leaves and depth

All leaves have the same depth.

#### Key count lower and upper bound

Every node has a lower and upper bound on the number of keys they can contain, which depends on a number $t \ge 2$ called the minimum degree.

$$
t - 1 \le |keys| \le 2t - 1
$$

and so from the node and children count relationship defined above, then

$$
t \le |children| \le 2t
$$

However, the root node has no lower bound for the key count or children count, but rather that if the tree is nonempty, it must have at least one key.

> [!note]
> We consider a node as full when it has exactly $2t - 1$ keys.

> [!note]
> We can call a specific B-Tree with some minimum degree $t$ as a $t$ - $2t$ tree, (e.g. a B-tree with minimum degree of $2$ is called a $2$-$3$-$4$ tree)

### Worst case complexities

| Operation | Worst case time complexity    |
| ------------- | ---------------------- |
| Retrieval        | $O(n)$      |
| Insertion     | $O(\log n)$ |
| Deletion      | $O(\log n)$ |

#### Worst case space complexity

$O(n)$

### Retrieval

Beginning at the root node, the retrieval procedure recurses as follows with the current node and target key as arguments:

#### Step 1 

Linearly search through the keys in the current node. The search in the current node stops under one of two conditions:
- Case 1: A key in the current node is found within some $i$ satisfying $0 \le i \le |keys| - 1$ such that it is greater than or equal to the target key.
- Case 2: All the keys in the current node have been checked, and no key was found that is greater than or equal to the target key.

#### Step 2

Once the search terminates, we proceed depending on the cases:
- Case 1: We now check if the key at index $i$ is exactly equal to the target key. If it's equal, the the lookup was successful and we return the node and the index $i$. Otherwise, (i.e. it was strictly greater than the target key), the algorithm must proceed to search deeper in the tree.
- Case 2: This means the all the keys in the current node is smaller than the target key. In this case, the algorithm must also search deeper in the tree.
If the linear search was unsuccessful, and the current node is not a leaf node, then we proceed to recurse on the child node at index $i$. Otherwise, if the current node is a leaf node, it means there are no more possible keys to check, and hence, it must be that the key is not in the   B-tree, so we return `None`.

### Insertion

Start from the root node. If it's full, that is, it contains $2t - 1$ keys, where $t$ is the minimum degree, create new root and set the old root as its child node...

TO DO

>[!note]
> Insertion occurs only at the leaf nodes.

### Deletion

TO DO

## Splay tree

TO DO
