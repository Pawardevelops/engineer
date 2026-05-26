# 29. Find First and Last Position of Element in Sorted Array

## Links

- LeetCode: [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return the first and last index of target in a sorted array, or [-1, -1] if missing.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Lower bound finds the first index where value is at least target. Another lower bound for target + 1 gives the position after the last target.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Scan from both ends or scan the whole array. That is O(n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Write a lower_bound helper.
2. Find start = lower_bound(target).
3. If start is out of range or not target, return [-1, -1].
4. Find end = lower_bound(target + 1) - 1.
5. Return [start, end].

## Dry Run

Use a small input for `Find First and Last Position of Element in Sorted Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        def lower_bound(value: int) -> int:
            left, right = 0, len(nums)
            while left < right:
                mid = (left + right) // 2
                if nums[mid] < value:
                    left = mid + 1
                else:
                    right = mid
            return left

        start = lower_bound(target)
        if start == len(nums) or nums[start] != target:
            return [-1, -1]

        end = lower_bound(target + 1) - 1
        return [start, end]
```

## Complexity Analysis

Time O(log n), space O(1).

## Common Mistakes

- Returning as soon as nums[mid] == target.
- Mixing inclusive and exclusive right boundaries.
- Not checking whether start actually points to target.

## What You Should Learn

Many sorted-array questions are really about finding the first index where a condition becomes true.
