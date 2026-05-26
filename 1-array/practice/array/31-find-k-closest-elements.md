# 31. Find K Closest Elements

## Links

- LeetCode: [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md), [Heap And Selection](../../patterns/heap-and-selection.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return k elements closest to x from a sorted array.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The answer is a contiguous window of length k. Binary search can choose the left boundary by comparing the left outside distance with the right outside distance.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Sort elements by distance to x and take k, then sort result. That ignores the original sorted structure.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Search possible window starts from 0 to n - k.
2. At mid, compare x - arr[mid] with arr[mid + k] - x.
3. If left side is farther, shift start right.
4. Otherwise keep mid or move left.
5. Return arr[left:left + k].

## Dry Run

Use a small input for `Find K Closest Elements` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

Suggested dry-run table:

| Step | Current Input Position | Important State | Decision | Why |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |

## Python Solution

```python
from typing import List


class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        left, right = 0, len(arr) - k

        while left < right:
            mid = (left + right) // 2

            if x - arr[mid] > arr[mid + k] - x:
                left = mid + 1
            else:
                right = mid

        return arr[left:left + k]
```

## Complexity Analysis

Time O(log(n - k) + k), space O(1) extra besides output slice.

## Common Mistakes

- Thinking selected elements can be non-contiguous after sorting.
- Using abs in a way that breaks tie preference for smaller values.
- Binary searching indexes beyond n - k.

## What You Should Learn

Sometimes the answer is a window, and binary search should target the window boundary.
