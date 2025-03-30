# Topological sorting

## Problem

> #### Definition (topological sort)
> A topological sort is a linear ordering of the vertices in a directed graph where for each directed edge from a vertex $u$ to vertex $v$, $u$ appears before $v$.

<img src="images/Pasted%20image%2020250303024845.png" width="400">

Given a directed acyclic graph, `dag`, return the topological sort of `dag`.

## Kahn's algorithm

### Idea

### Computational complexity

#### Time complexity

#### Space complexity

## Stack and depth-first search algorithm

### Idea

### Computational complexity

#### Time complexity

#### Space complexity

### Pseudocode

```
func topological_sort(graph: AdjacencyListGraph[V, E]) -> SinglyLinkedList[V] {
    var result: SinglyLinkedList[V] = SinglyLinkedList[V]::new();
    var visited: HashSet[V] = HashSet[V]::new();

    for vertex in graph.get_vertices() {
        if !visited.contains(vertex) {
            dfs_visit(graph, vertex, visited, result);
        }
    }

    return result;
}

func dfs_visit(graph: AdjacencyListGraph[V, E],
               vertex: V,
               visited: HashSet[V],
               result: SinglyLinkedList[V]) {

    visited.add(vertex);

    for neighbor in graph.get_neighbors(vertex) {
        if !visited.contains(neighbor) {
            dfs_visit(graph, neighbor, visited, result);
        }
    }

    result.add_first(vertex);
}
```
