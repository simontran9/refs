# Searching

## Problem

**Description**
Given an array `array` and a target element `target`, determine if `target` exists in array. If it does, return its index; otherwise, return `-1`.

**Input**
- An array `array` of elements
- A target element `target` to search for

**Output:**
- The index of target in `array` if found
- `-1` if target is not present in array

## Linear search

**Worst-case time complexity**
Worst-case $O(n)$

**Worst-case space complexity**
$O(1)$

**Pseudocode**
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

**Worst-case time complexity**
$O(\log n)$

**Worst-case space complexity**
- Iterative: $O(1)$ 
- Recursive: $O(\log n)$

**Pseudocode**
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

