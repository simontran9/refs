# Map and set

## Operations

### Map operations

| Operation                    | Description                                                                                                                                                                                                        |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `func get(key: K) -> V`      | Returns the value `v` associated with key `k`, if such an entry exists; otherwise returns `None`.                                                                                                                  |
| `func put(key: K, value: V)` | If the map does not have an entry with key equal to `k`, then adds entry `(k, v)` and returns `None` otherwise, replaces with `v` the existing value of the entry with key equal to `k` and returns the old value. |
| `func remove(key: K) -> K`   | Removes the entry with key equal to `k`, and returns its value `v`, but if the map has no such entry with key equal to `k`, then returns `None`.                                                                   |

### Set operations

| Operation                           | Description                                                                                              |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `func contains(element: E) -> Bool` | Returns `True` if the set contains element `e`, `False` otherwise.                                       |
| `func add(element: E) -> Bool`      | If the set does not already contain element `e`, adds `e` and returns `True`; otherwise returns `False`. |
| `func remove(element: E)`           | Removes element `e` from the set.                                                                        |

## Hash table container

### Retrieval

### Insertion

### Deletion

## Trie

### Retrieval

### Insertion

### Deletion



