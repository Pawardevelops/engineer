# 26. Search in Rotated Sorted Array

## Links

- LeetCode: [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find target in a sorted array that was rotated at an unknown pivot.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

At every middle point, at least one half is sorted. If the target is inside that sorted half, keep it; otherwise discard it.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Scan every element and return the matching index. That is O(n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Compute mid.
2. If nums[mid] is target, return mid.
3. Check whether the left half is sorted.
4. If target lies inside the sorted half, move toward it.
5. Otherwise search the other half.

## Dry Run

Use a small input for `Search in Rotated Sorted Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            if nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
```

## Complexity Analysis

Time O(log n), space O(1).

## Common Mistakes

- Assuming both halves are sorted.
- Using strict comparisons that exclude endpoints.
- Not handling the unrotated case.

## What You Should Learn

Binary search only needs enough order to safely discard one side.
