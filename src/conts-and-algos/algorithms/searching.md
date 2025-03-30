# Searching

## Problem

Given an array of elements, `array` and a target element, `target`, determine if `target` exists in `array`. If it does, return its index; otherwise, return `-1`.

## Linear search algorithm

### Idea

1. Start at the first element (index 0) of `array`
2. Compare the current element with `target`
3. If they match, return the current index. If they don't match, move to the next element
4. Repeat steps 2-3 until either:
   - A match is found, then return that index
   - The end of `array` is reached, then return `-1`

### Computational complexity

#### Time complexity

Worst-case: $O(n)$

#### Space complexity

Worst-case: $O(1)$

### Pseudocode

#### Pseudocode (iterative)

```
func iter_linear_search(array: Array[Int], target: Int) -> Int {
    for i in 0..array.len() {
        if array[i] == target {
            return i;
        }
    }

    return -1;
}
```

#### Pseudocode (recursive)

```
func rec_linear_search(array: Array[Int], target: Int, i: Int) -> Int {
    if array.is_empty() {
        return -1;
    }

    if array[i] == target {
        return i;
    }

    return rec_linear_search(array, target, i + 1);
}
```

## Binary search algorithm

### Idea

1. Initialize two pointers: `low` at the beginning of the array and `high` at the end
2. While `low` is less than or equal to `high`:
    - a. Calculate the middle index `mid` by getting the average of `low` and `high`
    - b. If the element at `mid` equals `target`, return `mid`
    - c. If the element at `mid` is less than `target`, update `low` to be `mid + 1`
    - d. If the element at `mid` is greater than `target`, update `high` to be `mid - 1`
3. If the while loop ends without finding `target`, return `-1`

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

