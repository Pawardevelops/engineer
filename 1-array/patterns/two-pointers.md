# Two Pointers

## Core Idea

Use two indexes to represent two useful positions in the same array. The pointers usually move toward each other, move in the same direction, or divide the array into processed and unprocessed regions.

## Why This Pattern Exists

Many brute force array solutions compare every pair. Two pointers keep only the pairs that can still matter and discard the rest using a sorted order, a boundary condition, or an invariant.

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

- The problem asks about pairs, triplets, ranges, or boundaries.
- The array is sorted, or sorting the array does not destroy the meaning of the answer.
- A decision at one pointer tells you which side can be safely ignored.
- You need an in-place overwrite pointer while scanning the array.

## When Not To Use It

- You need to remember arbitrary past values with no order relationship.
- Removing an element could make an earlier removed candidate valid again.
- The problem is really asking for all subsets or all permutations.

## Common Shapes

### Opposite direction
Start at both ends. Move the left pointer right or the right pointer left based on the current sum, area, or boundary.

### Same direction
Both pointers move forward. One pointer scans, the other marks the current write position or window start.

### Partition pointers
Maintain regions such as low, mid, and high when values must be rearranged in-place.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def two_sum_sorted(nums: List[int], target: int) -> list[int]:
    left, right = 0, len(nums) - 1

    while left < right:
        current = nums[left] + nums[right]

        if current == target:
            return [left, right]
        if current < target:
            left += 1
        else:
            right -= 1

    return []
```

## Worked Mini Examples

### Sorted pair sum
If current sum is too small, moving the left pointer is the only useful move because all values to its left are even smaller.

### Container area
The shorter wall limits the area, so moving the taller wall cannot improve the limiting height.

### Remove duplicates
A read pointer sees every value, and a write pointer keeps the compacted valid prefix.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Moving both pointers at once without proving both moves are safe.
- Forgetting duplicate skipping after finding a valid combination.
- Sorting when the original index order is required and not preserving indexes.

## Questions Using This Pattern

- [01. Container With Most Water](../practice/array/01-container-with-most-water.md)
- [02. Two Sum II - Input Array Is Sorted](../practice/array/02-two-sum-ii-input-array-is-sorted.md)
- [03. 3Sum](../practice/array/03-3sum.md)
- [04. 3Sum Closest](../practice/array/04-3sum-closest.md)
- [05. 4Sum](../practice/array/05-4sum.md)
- [06. Sort Colors](../practice/array/06-sort-colors.md)
- [07. Remove Duplicates From Sorted Array II](../practice/array/07-remove-duplicates-from-sorted-array-ii.md)
