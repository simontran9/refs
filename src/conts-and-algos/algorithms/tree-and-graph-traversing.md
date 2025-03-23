# Tree and graph traversing

https://www.cs.mcgill.ca/~jeromew/teachings/251/F2022/COMP251_Lecture4_F2022.pdf

## Tree traversing problem

Given a root node of a rooted tree, `root`, traverse the the rooted tree in a pre-order, in-order, post-order, or level-order fashion.

## Tree depth-first search (pre-order,  in-order,  post-order) algorithm

### Idea

### Computational complexity

#### Time complexity

Worst-case: $O(n)$

#### Space complexity

Worst-case: $O(n)$

### Pseudocode

#### Pseudocode (pre-order traversal)

```
func recursive_dfs(root: BinaryTreeNode[K]) {
    if root == None {
        return; 
    }
    // visit e.g. println("{}", root.key);
    recursive_dfs(root.left);
    recursive_dfs(root.right);
}
```

```
func iterative_dfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return; 
    }

    var stack: ArrayStack[BinaryTreeNode[K]] = ArrayStack[BinaryTreeNode[K]]::new();
    var current: BinaryTreeNode[K] = root;

    while !stack.is_empty() or current != None {
        if current != None {
            // visit e.g. println("{}", current.key);
            stack.push(current.right);
            current = current.left;
        } else {
            current = stack.pop();
        }
    }
}
```

#### Pseudocode (in-order traversal)

```
func recursive_dfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return; 
    }
    recursive_dfs(root.left);
    // visit e.g. println("{}", root.key);
    recursive_dfs(root.right);
}
```

```
func iterative_dfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return; 
    }

    var stack: ArrayStack[BinaryTreeNode[K]] = ArrayStack[BinaryTreeNode[K]]::new();
    var current: BinaryTreeNode[K] = root;

    while !stack.is_empty() or current != None {
        if current != None {
            stack.push(current);
            current = current.left;
        } else {
            current = stack.pop();
            // visit e.g. println("{}", current.key);
            current = current.right;
        }
    }
}
```

#### Pseudocode (post-order traversal)

```
func recursive_dfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return;
    }
    recursive_dfs(root.left);
    recursive_dfs(root.right);
    // visit e.g. println("{}", root.key);
}
```

```
func iterative_dfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return; 
    }

    var stack: ArrayStack[BinaryTreeNode[K]] = ArrayStack[BinaryTreeNode[K]]::new();
    var current: BinaryTreeNode[K] = root;
    var last_visited: BinaryTreeNode[K] = None;

    while !stack.is_empty() or current != None {
        if current != None {
            stack.push(current);
            current = current.left;
        } else {
            var peek_node: BinaryTreeNode[K] = stack.top();

            if peek_node.right != None and peek_node.right != last_visited {
                current = peek_node.right;
            } else {
                // visit e.g. println("{}", peek_node.key);
                last_visited = stack.pop();
                current = None;
            }
        }
    }
}
```

## Tree breadth-first search (level-order) algorithm

### Idea

### Computational complexity

#### Time complexity

Worst-case: $O(n)$

#### Space complexity

Worst-case: $O(n)$

### Pseudocode

```
func iterative_bfs(root: BinaryTreeNode[K]) {
    if root == None { 
        return; 
    }
    
    queue: ArrayQueue[BinaryTreeNode[K]] = ArrayQueue[BinaryTreeNode[K]]::new();
    queue.enqueue(root);

    while !queue.is_empty() {
        var current: BinaryTreeNode[K] = queue.dequeue();
        // visit e.g. println("{}", current.key);
        if current.left != None { 
            queue.enqueue(current.left); 
        }
        if current.right != None { 
            queue.enqueue(current.right); 
        }
    }
}
```

## Graph traversing problem

Given a graph, `graph`, and a source node of `graph`, `source`, traverse `graph` beginning at the `source`.

## Graph depth-first search

### Idea

<img src="images/Pasted%20image%2020250318064132.png" width="300">

TO DO

### Computational complexity

#### Time complexity

Worst-case: $O(|V| + |E|)$

#### Space complexity

Worst-case: $O(V)$

### Pseudocode

#### Pseudocode (iterative)

```
func iterative_dfs(graph: AdjacencyListGraph[V, E], source: V) {
    var visited: HashSet[V] = HashSet[V]::new();
    var stack: ArrayStack[V] = ArrayStack[V]::new();
    
    stack.push(source);
    
    while !stack.is_empty() {
        var vertex: V = stack.pop();
        if !visited.contains(vertex) {
            visited.add(vertex);
            for neighbor in graph.get_neighbors(vertex) {
                stack.push(neighbor);
            }
        }
    }
}
```

#### Pseudocode (recursive)

```
func recursive_dfs(graph: AdjacencyListGraph[V, E], vertex: V, visited: HashSet[V]) {
    visited.add(vertex);

    for neighbor in graph.get_neighbors(vertex) {
        if !visited.contains(neighbor) {
            recursive_dfs(graph, neighbor, visited);
        }
    }
}
```

## Graph breadth-first search

### Idea

<img src="images/Pasted%20image%2020250318064110.png" width="300">

TO DO

### Computational complexity

#### Time complexity

Worst-case: $O(|V| + |E|)$

#### Space complexity

Worst-case: $O(V)$

### Pseudocode

```
func iterative_bfs(graph: AdjacencyListGraph[V, E], source: V) {
    var visited: HashSet[V] = HashSet[V]::new();
    var queue: ArrayQueue[V] = ArrayQueue[V]::new();
    
    queue.enqueue(source);
    visited.add(source);
    
    while !queue.is_empty() {
        var vertex: V = queue.dequeue();
        for neighbor in graph.get_neighbors(vertex) {
            if !visited.contains(neighbor) {
                visited.add(neighbor);
                queue.enqueue(neighbor);
            }
        }
    }
}
```
