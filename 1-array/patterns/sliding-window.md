# Sliding Window

## Core Idea

Maintain a contiguous range of the array and update its state as the right boundary expands and the left boundary shrinks.

## Why This Pattern Exists

A brute force solution recomputes every subarray from scratch. Sliding window reuses almost all previous work because adjacent windows differ by only a few elements.

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

- The problem asks for a longest, shortest, or counted contiguous subarray.
- All numbers are non-negative, or the window condition is monotonic as the window expands.
- You can update the answer by adding one right element and removing left elements.
- The constraint says subarray, substring, or consecutive segment.

## When Not To Use It

- Negative numbers break the monotonic relationship between window size and sum.
- The chosen elements do not need to be contiguous.
- The best decision depends on many past states, which usually points to dynamic programming.

## Common Shapes

### Fixed size
The window length is fixed. Add the new right element and remove the element that falls out.

### Variable size max
Expand right, then shrink left while the window is invalid. Record the largest valid window.

### Variable size min
Expand right until valid, then shrink left while staying valid. Record the smallest valid window.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def longest_window_at_most_k_bad(nums: List[int], k: int) -> int:
    left = 0
    bad = 0
    best = 0

    for right, value in enumerate(nums):
        if value == 0:
            bad += 1

        while bad > k:
            if nums[left] == 0:
                bad -= 1
            left += 1

        best = max(best, right - left + 1)

    return best
```

## Worked Mini Examples

### Minimum size subarray sum
With positive numbers, once the sum is large enough, shrinking may reveal a shorter valid window.

### At most K zeros
The window is valid while the number of zeros is at most K.

### Product less than K
With positive numbers, product grows when expanding and shrinks when moving left.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Using sliding window on arrays with negative numbers when prefix sums are needed.
- Updating the answer before restoring the invariant.
- Shrinking only once when the window may still be invalid.

## Questions Using This Pattern

- [14. Minimum Size Subarray Sum](../practice/array/14-minimum-size-subarray-sum.md)
- [15. Subarray Product Less Than K](../practice/array/15-subarray-product-less-than-k.md)
- [16. Fruit Into Baskets](../practice/array/16-fruit-into-baskets.md)
- [17. Max Consecutive Ones III](../practice/array/17-max-consecutive-ones-iii.md)
- [18. Minimum Operations to Reduce X to Zero](../practice/array/18-minimum-operations-to-reduce-x-to-zero.md)
