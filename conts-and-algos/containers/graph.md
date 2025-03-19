# Graph

## Terminology

**Basic terminology**
- Graph: a pair $G = (V, E)$ where $V$ is a set of nodes, called vertices and $E \subseteq V \times V$ is a collection of pairs of vertices, called edges
- Directed edge: an ordered pair of vertices $(u, v)$, where the first vertex $u$ is the origin and second vertex $v$ is the destination, denoted $u \to v$
- Undirected edge: an unordered pair of vertices $(u, v)$ i.e. for all $v$, $(u, v) = (v, u)$
- Unweighted edge: an edge which has no associated real number
- Weighted edge: an edge that has an associated real number $k \in \mathbb{R}$, given by a weight function $w: E \to \mathbb{R}$

**Types of graphs**
- Undirected graph: a graph where all edges are undirected, and contains no self-loops and no parallel edges
- Directed graph (a.k.a digraph): a graph where all edges are directed, and may contain self-loops
- Acyclic graph: a directed graph that has no directed cycles
- Cyclic graph: a graph that contains a cycle
- Unweighted graph: a graph where all edges are unweighted
- Weighted graph: a graph where all edges have weights
- Dense graph: a graph with a high number of edges relative to the maximum possible number of edges i.e. $|E| \approx |V|^2$
- Sparse graph: a graph with relatively few edges compared to the maximum possible number of edges i.e. $|E| \ll |V|^2$
- Connected graph: a graph where for all pairs of vertices $u$ and $v$, there is a path between $u$ and $v$
- Strongly connected graph: a directed graph where for any two vertices $u$ and $v$ , $u$ reaches $v$ and $v$ reaches $u$
- Subgraph: a graph whose vertices and edges are subsets of the vertices and edges of a larger graph
- Spanning subgraph: a subgraph of some graph $G$ that contains all the vertices of $G$
- Connected components: the maximal connected subgraphs of a larger graph that isn't connected
- Forest: an undirected acyclic graph, where each of its connected components is a tree
- Spanning tree: a spanning subgraph that is a tree

**Vertices and edges terminology**
- Endpoint of an edge: two vertices at the extremity of some edge (e.g. $U$ and $V$ are the endpoints of $a$)
- Edges incident on a vertex: edges coming out of a common vertex (e.g. $a$, $b$, and $d$ are incident on $V$)
- Adjacent vertices: vertices connected by an edge (e.g. $U$ and $V$ are adjacent)
- Ingoing edge: an edge directed toward a vertex
- Outgoing edge: an edge directed away from a vertex
- Degree of a vertex: number of incident edges (e.g. $X$ has degree 5), denoted $deg(u)$
- In-degree: number of edges directed toward a vertex, denoted $in(u)$
- Out-degree: number of edges directed away from a vertex, denoted $out(u)$
- Parallel edges: edges which have the same endpoints (e.g. $h$ and $i$ are parallel edges)
- Self-loop: an edge that connects a vertex to itself (e.g. $j$ is a self-loop)
![](images/Pasted%20image%2020250318002242.png)

**Path terminology**
- Path: a sequence of adjacent vertices $(v_1 , v_2, \dots, v_k)$ such that $(v_i, v_{i + 1})$ is an edge
- Simple path: path such that all its vertices are distinct (e.g. $P_1 = (V, X, Z)$ is a simple path, but not $P_2 = (U, W, X, Y, W, V)$)
- Path length: the number of edges in the path, or equivalently, number of vertices in the path minus one
![](images/Pasted%20image%2020250318003131.png)
**Cycle terminology**
- Cycle: a path that starts and ends at the same vertex
- Simple cycle: a cycle where each vertex is distinct (e.g. $C_1 = (V, X, Y, W, U, V)$ is a simple cycle, but not $C_2 = (U, W, X, Y, W, V, U)$)
![](images/Pasted%20image%2020250318003316.png)

**Tree terminology**
- Tree: an undirected connected acyclic graph
- Free tree: a tree with no designated root node
- Rooted tree: a tree in which one vertex has been designated the root
- Subtree: a smaller tree entirely contained within a larger tree, with a node from the original tree serving as its root, and including all its descendants
- Root node: the topmost node in the tree
- Parent node: a node with one or more child nodes
- Child node: a node pointed by a single node above (its parent), except the root
- Sibling node: a node with the same parent
- Oldest child: the leftmost child node of some parent node
- Leaf/external node: a node without children nodes
- Internal node: a node with children nodes
- Ancestor and descendent of a node:  $v$ is an ancestor of $w$ if there is a path from $v$ to $w$, while $v$ would be considered the descendent of $w$
- Depth/level of a node: the number of edges from the root to the node
- Height of a node: the number of edges from the node to the deepest leaf
- Height of a tree: the height of the root node
- $m$-ary tree: a rooted tree where every node has at most $m$ children
- Binary tree: a rooted tree for which every node has at most two child nodes
- Binary search tree: a binary tree which satisfy the BST invariant, which states that for every node $x$, all nodes to the left of $x$ must have a key less than $x$'s key, while all nodes to the right must have a key greater than $x$'s key
- Full tree: a rooted tree in which each node has exactly $0$ or $N$ children
- Complete tree: a rooted tree for which all the levels are filled, with the possible exception of the last level, which is filled from left to right

## Properties

> **Proposition (sum of degrees)**
>
> If $G = (V, E)$ is a graph, then
> $$
> \sum_{v \in V} deg(v) =2|E|
> $$

> **Proposition (in and out degrees count)**
>
> If $G = (V, E)$ is a directed graph, then
> $$
> \sum_{v \in V} in(v) = \sum_{v \in V} out(v) = |E|
> $$

> **Proposition (maximum edge count)**
>
> For an undirected graph, the following holds
> $$
> |E| \le \frac{|V|(|V| - 1)}{2}
> $$
> and for a directed graph, the following holds
> $$
>|E| \le |V|(|V| - 1)
> $$
> $\therefore |E| = O(|V|^2)$

> **Proposition (edge count of undirected graphs)**
>
> If a graph $G$ is an undirected graph, and
> - if $G$ is connected, then $|E| ≥ |V| - 1$
> - if $G$ is a tree, then $|E| = |V| - 1$
> - if $G$ is a forest, then $|E| \le |V| - 1$

## Operations

| **Operation**                                          | **Description**                                                             |
| ------------------------------------------------------ | --------------------------------------------------------------------------- |
| `func get_vertices() -> ArrayList[V]`                  | Retrieves all the vertices present in the graph.                            |
| `func get_edges() -> ArrayList[E]`                     | Retrieves all the edges present in the graph.                               |
| `func get_neighbors(vertex: V) -> Array[V]`            | Returns a list of neighboring vertices connected to the specified vertex.   |
| `func add_vertex(vertex: V)`                           | Adds a new vertex to the graph.                                             |
| `func add_edge(vertex_1: V, vertex_2: V, weight: Int)` | Creates a new edge between `vertex_1` and `vertex_2` with the given weight. |
| `func contains_vertex(vertex: V) -> Bool`              | Checks if the specified vertex exists in the graph.                         |
| `func contains_edge(vertex_1: V, vertex_2: V) -> Bool` | Checks if an edge exists between `vertex_1` and `vertex_2`.                 |
| `func remove_vertex(vertex: V)`                        | Removes the specified vertex and all associated edges from the graph.       |
| `func remove_edge(vertex_1: V, vertex_2: V)`           | Removes the edge between `vertex_1` and `vertex_2` from the graph.          |

> [!note]
> Getting and setting vertex value and/or edge weight is allowed

## Adjacency list

![](images/Pasted%20image%2020250318004431.png)

> [!note]
> For a weighted graph, store the weights alongside the vertices in the list

### Worst case complexities

**Worst case time complexity**

| **Operation**                      | **Worst case time complexity** |
| ---------------------------------- | ------------------------------ |
| Get all vertices                   | $O(V)$                         |
| Get all edges                      | $O(V + E)$                     |
| Get all neighbors of a vertex      | $O(V)$                         |
| Inserting (vertex)                 | $O(1)$                         |
| Insertion (edge)                   | $O(1)$                         |
| Checking the existence of a vertex | $O(1)$                         |
| Checking the existence of an edge  | $O(V)$                         |
| Deletion (vertex)                  | $O(\|V\| + \|E\|)$             |
| Deletion (edge)                    | $O(V)$                         |

**Worst case space complexity**

$O(|V| + |E|)$

### Search


**Check if there's an edge**

Search through the associated list of `vertex1` for `vertex2`. If `vertex2` is found, return `True`, otherwise, return `False`.

### Insertion

**Vertex insertion**

Create a new entry in the hash table, where the key is the vertex, and the value is an empty list (either an array list or a linked list).

**Edge insertion**

For two vertices, `vertex1` and `vertex2`, add `vertex2` to the associated list of `vertex1`'s entry, and add `vertex1` to the associated list of `vertex2's` entry

### Deletion

## Adjacency matrix

![](images/Pasted%20image%2020250318004446.png)

> [!note]
> $A = A^T$ for undirected graphs

> [!note]
> For a weighted graph, store the weights instead of bits.

### Worst case complexities

**Worst case time complexity**

| **Operation**                          | **Worst case time complexity** |
| -------------------------------------- | ------------------------------ |
| `get_vertices()`                       | $O(V)$                         |
| `get_edges()`                          | $O(\|V\|^2)$                   |
| `get_neighbors(vertex)`                | $O(V)$                         |
| `add_vertex(vertex)`                   | $O(\|V\|^2)$                   |
| `add_edge(vertex_1, vertex_2, weight)` | $O(1)$                         |
| `contains_vertex(vertex)`              | $O(1)$                         |
| `contains_edge(vertex_1, vertex_2)`    | $O(1)$                         |
| `remove_vertex(vertex)`                | $O(\|V\|^2)$                   |
| `remove_edge(vertex_1, vertex_2)`      | $O(1)$                         |

**Worst case space complexity**

$O(|V|^2)$

### Search

### Insertion

**Edge insertion**

Set `adjacency_matrix[i][j]` to `1`.

### Deletion

**Edge deletion**

Set `adjacency_matrix[i][j]` to `0`

> [!tip] When to use adjacency list vs adjacency matrix
>
> - Choose adjacency lists if:
> 	- You frequently need to add/remove vertices
> 	- The graph is sparse (space-efficient)
> 	- Need to traverse the graph
> - Choose adjacency matrices if:
> 	- You frequently need to add or remove edges, but *not* vertices
> 	- You frequently need to check for the presence or absence of an edge between $i$ and $j$
> 	- Matrix is small enough to fit in memory

