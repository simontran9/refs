# Searching

## Problem

Given an array of elements, `array` and a target element, `target`, determine if `target` exists in `array`. If it does, return its index; otherwise, return `-1`.

## Linear search

### Idea

TO DO

### Computational complexity

#### Time complexity

Worst-case: $O(n)$

#### Space complexity

Worst-case: $O(1)$

### Pseudocode

```
func linear_search(array: Array[Int], target: Int) -> Int {
    for i in 0..array.len() {
        if array[i] == target {
            return i;
        }
    }
    
    return -1;
}
```

## Binary search

### Idea

TO DO

### Computational complexity

#### Time complexity

Worst-case: $O(\log n)$

#### Space complexity

- Worst-case (iterative): $O(1)$ 
- Worst-case (recursive): $O(\log n)$

### Pseudocode

#### Pseudocode (iterative)

```
func iterative_binary_search(array: Array[Int], target: Int) -> Int {
    var low: Int = 0;
    var high: Int = array.len() - 1;
    
    while low <= high {
        var mid: Int = low + (high - low) / 2;
        if array[mid] == target {
            return mid;
        } else if array[mid] < target {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return -1;
}
```

#### Pseudocode (recursive)

```
func recursive_binary_search(array: Array[Int], low: Int, high: Int, target: Int) -> Int {
    if low <= high {
        mid: Int = low + (high - low) / 2;
        if array[mid] == target {
            return mid;
        } else if array[mid] < target {
            return recursive_binary_search(array, mid + 1, high, target);
        } else {
            return recursive_binary_search(array, low, mid - 1, target);
        }
    }
    
    return -1;
}
```

