# Sorting

## Problem

### Description

Given an array of elements, `array`, sort it in non-decreasing order.

### Input

An array of elements, `array`.

### Output

- If the sorting is in-place, return nothing, but rather, the original array should be modified so that its elements are sorted in non-decreasing order.
- If the sorting is not in-place, return a new array that is a sorted version of original array, leaving the original unchanged.

## Bubble sort

### Idea

1. Begin at the first element
2. Continuously swap two adjacent elements so the smaller element is before the larger element
3. Repeat step 1 to step 2 until the array is completely sorted

<img src="images/Pasted%20image%2020250303030750.png" width="500">

### Computational complexity

#### Time complexity 

Worst-case: $O(n^2)$

#### Space complexity

Worst-case: $O(1)$

### Properties

- Stable
- In-place

### Pseudocode

```
func bubble_sort(array: Array[Int]) {
    var swapped: Bool = False;
    for i in 0..(array.len() - 1) {
        for j in 0..(array.len() - i - 1) {
            if array[j] > array[j + 1] {
                array.swap(j, j + 1);
                swapped = True;
            }
        }
        if !swapped {
            break; 
        }
    }
}
```

## Selection sort

### Idea

1. Go through the array to find the smallest element
2. Move the smallest element to the front of the unsorted portion of the array
3. Repeat step 1 and step 2 until the array is completely sorted

<img src="images/Pasted%20image%2020250226031346.png" width="300">

### Computational complexity

#### Time complexity 

Worst-case: $O(n^2)$

#### Space complexity

Worst-case: $O(1)$

### Properties

- Not stable
- In-place

### Pseudocode

```
func selection_sort(array: Array[Int]) {
    for i in 0..(array.len() - 1) {
        var min_index: Int = i;
        for j in (i + 1)..array.len() {
            if array[j] < array[min_index] {
                min_index = j;
            }
        }
        if min_index != i {
            array.swap(min_index, i);
        }
    }
}
```

## Insertion sort

### Idea

1. Start with the second element
2. Compare the current element with the previous elements in the sorted portion and insert it into the correct position in the sorted portion
3. Select the next element in the unsorted portion of the array
4. Repeat step 2 to step 3 until the array is completely sorted

<img src="images/Pasted%20image%2020250226022041.png" width="500">

### Computational complexity

#### Time complexity 

Worst-case: $O(n^2)$

#### Space complexity

Worst-case: $O(1)$

### Properties

- Stable
- In-place

### Pseudocode

```
func insertion_sort(array: Array[Int]) {
    for i in 1..array.len() {
        const current: Int = array[i];
        var j: Int = i - 1;
        while j >= 0 and array[j] > current {
            array[j + 1] = array[j];
            j -= 1;
        }
        array[j + 1] = current;
    }
}
```

## Merge sort

### Idea

1. Repeatedly split the array in half until you have subarrays containing single elements (these are inherently sorted)
2. Merge adjacent subarrays in a way that maintains sorted order, comparing elements from each subarray
3. Continue merging larger and larger subarrays until the entire array is sorted

<img src="images/Pasted%20image%2020250303032958.png" width="300">

### Computational complexity

#### Time complexity 

Worst-case: $O(n \log n)$

#### Space complexity

Worst-case: $O(1)$

### Properties

- Stable
- Not in-place

### Pseudocode

```
func merge_sort(array: Array[Int]) -> Array[Int] {
    if array.len() <= 1 { 
        return array; 
    }

    const mid: Int = array.len() / 2;
    left: Array[Int] = array[0..mid];
    right: Array[Int] = array[mid..array.len()];

    left = merge_sort(left);
    right = merge_sort(right);

    return merge(left, right);
}

func merge(left: Array[Int], right: Array[Int]) -> Array[Int] {
    var left_index: Int = 0;
    var right_index: Int = 0;
    var merged: ArrayList[Int] = ArrayList[Int]::new();

    while left_index < left.len() and right_index < right.len() {
        if left[left_index] < right[right_index] {
            merged.add_last(left[left_index]);
            left_index += 1;
        } else {
            merged.add_last(right[right_index]);
            right_index += 1;
        }
    }

    while left_index < left.len() {
        merged.add_last(left[left_index]);
        left_index += 1;
    }
    
    while right_index < right.len() {
        merged.add_last(right[right_index]);
        right_index += 1;
    }

    return merged;
}
```

## Randomized quick sort

### Partitioning schemes

#### Lomuto's partition scheme

1. Select a random element as the pivot
2. Move the random pivot to the end of the array
3. We'll use a variable `i` to track the boundary of elements smaller than the pivot. Initialize it to the position before the first element (typically `low - 1`).
4. We'll use another variable `j` to scan through the array from the first element to the second-to-last element.
5. For each position `j`:
    - If the current element is less than or equal to the pivot:
        - Increment `i` (expanding the "smaller than pivot" region)
        - Swap the elements at positions `i` and `j`
    - If the current element is greater than the pivot:
        - Do nothing and continue to the next element
6. After we've finished scanning the array (when `j` reaches the end):
    - Swap the pivot (which is at the last position) with the element at position `i + 1`
    - Return `i + 1` as the final position of the pivot
7. Apply quick sort recursively to the left subarray and the right subarray about the partitioning index (where in this partition scheme, the pivot index is the partitioning index)

<img src="images/Pasted%20image%2020250317040244.png" width="300">

#### Hoare's partition scheme

1. Select a random element as the pivot
2. Move the random pivot to the first position of the array (typically position `low`)
3. Initialize two pointers:
    - `i` starting at `low - 1` (just before the first element)
    - `j` starting at `high + 1` (just after the last element)
4. Repeat until `i` and `j` cross each other:
    - Increment `i` and continue incrementing it while the element at position `i` is less than the pivot
    - Decrement `j` and continue decrementing it while the element at position `j` is greater than the pivot
    - If `i` and `j` haven't crossed yet, swap the elements at positions `i` and `j`
5. When `i` and `j` cross:
    - Return `j` as the partitioning index
6. Apply quick sort recursively:
    - To the left subarray (`low` to the returned partitioning index)
    - To the right subarray (the partitioning_index + 1 to `high`)

> [!note]
> Lomuto's partition scheme will partition the array such that:
> - Elements less than or equal to the pivot go to its left
> - Elements greater than the pivot go to its right
> - The pivot is in its final sorted position
> 
> While Hoare's partition scheme will partition the array such that:
> - Elements less than or equal to the pivot are in the left partition (`array[low...j]`)
> - Elements greater than or equal to the pivot are in the right partition (`array[j + 1...high]`)
> - The pivot element itself could be in either partition
> - The pivot is *not* guaranteed to be in its final sorted position
> - The partitioning index `j` is returned, which acts as the boundary between partitions

> [!note]
> Lomuto's partition scheme will place the pivot as the last element, while Hoare's partition scheme will place the pivot as the first element

### Computational complexity

#### Time complexity 

- Worst-case: $O(n^2)$
- Average-case: $O(n \log n)$

#### Space complexity

- Worst-case: $O(n^2)$
- Average-case: $O(n \log n)$

### Properties

- Not stable
- In-place

### Pseudocode 

#### Pseudocode (randomized quick sort with Lomuto's partition scheme)

```
import random;

func quick_sort(array: Array[Int], low: Int, high: Int) {
    if low < high { 
        const pi: Int = lomuto_partition(array, low, high);
        quick_sort(array, low, pi - 1);
        quick_sort(array, pi + 1, high);
    }
}

func lomuto_partition(array: Array[Int], low: Int, high: Int) -> Int {
    const pivot: Int = lomuto_pivot_selection(array, low, high);

    var i: Int = low - 1;

    for j in low..high {
        if array[j] <= pivot {
            i += 1;
            array.swap(i, j);
        }
    }

    array.swap(i + 1, high);

    return i + 1;
}

func lomuto_pivot_selection(array: Array[Int], low: Int, high: Int) -> Int {
    const i: Int = low + random::int(0, high - low + 1);
    array.swap(i, high);
    return array[high];
}
```

#### Pseudocode (randomized quick sort with Hoare's partition scheme)

```
import random;

func quick_sort(array: Array[Int], low: Int, high: Int) {
    if low >= high {
        return;
    }
    const pi: Int = hoare_partition(array, low, high);
    quick_sort(array, low, pi);
    quick_sort(array, pi + 1, high);
}

func hoare_partition(array: Array[Int], low: Int, high: Int) -> Int {
    const pivot: Int = hoare_pivot_selection(array, low, high);
    var i: Int = low - 1;
    var j: Int = high + 1;
    
    while True {
        i += 1;
        while i < high and array[i] < pivot {
            i += 1;
        }
        
        j -= 1;
        while j > low and array[j] > pivot {
            j -= 1;
        }
        
        if i >= j {
            return j;
        }
        
        array.swap(i, j);
    }
}

func hoare_pivot_selection(array: Array[Int], low: Int, high: Int) -> Int {
    const i: Int = low + random::int(0, high - low);
    array.swap(i, low);
    return array[low];
}
```

## Heap sort

### Idea

1. Build a max heap from the input array
2. Select the last slot from the unsorted portion of the array
3. Change the element in the last slot to the top element in the heap
4. Remove the top element from the heap
5. Repeat step 2 and step 4 until the array is completely sorted

<img src="images/Pasted%20image%2020250226053913.png" width="300">
<img src="images/Pasted%20image%2020250226054010.png" width="300">
<img src="images/Pasted%20image%2020250226054025.png" width="300">
<img src="images/Pasted%20image%2020250226054034.png" width="300">
<img src="images/Pasted%20image%2020250226054047.png" width="300">

### Computational complexity 

#### Time complexity

Worst-case: $O(n \log n)$

#### Space complexity

Worst-case: $O(1)$

### Properties

- Not stable
- In-place

### Pseudocode

```
func heap_priority_queue_sort(array: Array[Int]) {
    var pq: MaxHeapPriorityQueue[Int] = MaxHeapPriorityQueue[Int]::from(array);
    for i in (0..pq.len()).rev() {
        array[i] = pq.remove_top();
    }
}
```
