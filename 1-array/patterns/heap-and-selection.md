# Heap And Selection

## Core Idea

Find the top k, kth largest, or most frequent elements without fully sorting everything when full order is unnecessary.

## Why This Pattern Exists

Sorting gives complete order, but many questions only need a small part of that order. Heaps, buckets, and quickselect focus the work.

The pattern is useful because it gives you a repeatable way to answer this question:

```text
What information do I keep so I do not repeat work?
```

For array problems, the repeated work is usually one of these:

- Checking the same pair or range again
- Recomputing a subarray property from the beginning
- Searching for a value that could have been remembered
- Revisiting cells, intervals, or candidates that can already be ruled out

## When To Use It

- The question asks for top k, kth largest, or k closest.
- You only need partial order.
- Frequencies matter more than original order.
- The array can be partitioned around a pivot.

## When Not To Use It

- The output must be fully sorted and stable.
- k is almost n and sorting is simpler enough.
- Worst-case guarantees are strict and randomized quickselect is not acceptable.

## Common Shapes

### Min-heap of size k
Keep only the best k seen so far.

### Bucket by frequency
Use counts as indexes when frequency is at most n.

### Quickselect
Partition until the kth position is fixed.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from heapq import heappush, heappushpop
from typing import List


def top_k_largest(nums: List[int], k: int) -> List[int]:
    heap = []

    for value in nums:
        if len(heap) < k:
            heappush(heap, value)
        elif value > heap[0]:
            heappushpop(heap, value)

    return heap
```

## Worked Mini Examples

### Top K frequent
Bucket frequencies from high to low until k values are collected.

### Kth largest
Quickselect finds the target rank without fully sorting.

### K closest elements
Binary search plus slicing can beat heap when the array is sorted.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Sorting the entire array when k is small and constraints are large.
- Forgetting that Python heapq is a min-heap.
- Returning elements in sorted order when the problem says any order is allowed.

## Questions Using This Pattern

- [20. Top K Frequent Elements](../practice/array/20-top-k-frequent-elements.md)
- [21. Kth Largest Element in an Array](../practice/array/21-kth-largest-element-in-an-array.md)
- [31. Find K Closest Elements](../practice/array/31-find-k-closest-elements.md)
