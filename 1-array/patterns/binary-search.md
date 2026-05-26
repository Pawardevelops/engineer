# Binary Search On Arrays

## Core Idea

Repeatedly cut a sorted or partially ordered search space in half while preserving the side that can still contain the answer.

## Why This Pattern Exists

When an array has order, checking the middle can eliminate many impossible positions at once.

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

- The array is sorted.
- The array is rotated sorted but one half is still sorted.
- The problem asks for first, last, minimum, peak, or exact position.
- A local comparison tells which side must contain an answer.

## When Not To Use It

- There is no monotonic or ordered property.
- You cannot prove which half is safe to discard.
- The array is tiny and clarity matters more than logarithmic time.

## Common Shapes

### Exact search
Return when nums[mid] equals target.

### Boundary search
Find the first index where a condition becomes true.

### Rotated search
Identify the sorted half, then decide if the target lies inside it.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def lower_bound(nums: List[int], target: int) -> int:
    left, right = 0, len(nums)

    while left < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid

    return left
```

## Worked Mini Examples

### Search in rotated array
At least one half is sorted, so target membership in that half is testable.

### First and last position
Two lower-bound searches find the range edges.

### Find peak
If the slope rises to the right, a peak exists on the right side.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Using `right = len(nums) - 1` in a lower-bound template without adjusting loop rules.
- Not handling duplicates when duplicates change the discard logic.
- Returning mid before deciding whether first or last occurrence is required.

## Questions Using This Pattern

- [26. Search in Rotated Sorted Array](../practice/array/26-search-in-rotated-sorted-array.md)
- [27. Find Minimum in Rotated Sorted Array](../practice/array/27-find-minimum-in-rotated-sorted-array.md)
- [28. Find Peak Element](../practice/array/28-find-peak-element.md)
- [29. Find First and Last Position of Element in Sorted Array](../practice/array/29-find-first-and-last-position-of-element-in-sorted-array.md)
- [30. Single Element in a Sorted Array](../practice/array/30-single-element-in-a-sorted-array.md)
- [31. Find K Closest Elements](../practice/array/31-find-k-closest-elements.md)
