# Sorting-Based Array Patterns

## Core Idea

Sort the array to create order, group equal values, or make greedy and two-pointer decisions possible.

## Why This Pattern Exists

Sorting costs O(n log n), but it can remove a much larger O(n^2) or O(n^3) search by exposing structure.

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

- The output does not depend on original order, or you can preserve original indexes separately.
- You need to group duplicates.
- You need to compare neighbors after ordering.
- A greedy choice becomes obvious once values are sorted.

## When Not To Use It

- The question explicitly requires original relative order.
- There is an O(n) counting, hashing, or in-place option that is expected.
- Values have huge objects where sorting is expensive and unnecessary.

## Common Shapes

### Sort then two pointers
Used for sum combinations like 3Sum and 4Sum.

### Sort then scan
Used for intervals, h-index, and duplicate grouping.

### Sort then binary search
Used when choosing a position or distance after ordering.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def pair_sums_after_sort(nums: List[int], target: int) -> list[tuple[int, int]]:
    nums.sort()
    left, right = 0, len(nums) - 1
    pairs = []

    while left < right:
        total = nums[left] + nums[right]
        if total == target:
            pairs.append((nums[left], nums[right]))
            left += 1
            right -= 1
        elif total < target:
            left += 1
        else:
            right -= 1

    return pairs
```

## Worked Mini Examples

### 3Sum
Sorting makes duplicate skipping and left/right movement possible.

### Merge intervals
Sorting by start means overlapping intervals appear next to each other.

### H-index
Sorting citations makes it easy to test h papers with at least h citations.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Forgetting that sorting changes indexes.
- Skipping duplicates before recording a valid answer.
- Sorting when a linear solution is available and required by constraints.

## Questions Using This Pattern

- [03. 3Sum](../practice/array/03-3sum.md)
- [04. 3Sum Closest](../practice/array/04-3sum-closest.md)
- [05. 4Sum](../practice/array/05-4sum.md)
- [25. H-Index](../practice/array/25-h-index.md)
- [34. Magnetic Force Between Two Balls](../practice/array/34-magnetic-force-between-two-balls.md)
- [35. Merge Intervals](../practice/array/35-merge-intervals.md)
