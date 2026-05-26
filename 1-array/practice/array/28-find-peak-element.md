# 28. Find Peak Element

## Links

- LeetCode: [Find Peak Element](https://leetcode.com/problems/find-peak-element/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return an index of any element that is greater than its neighbors.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If nums[mid] < nums[mid + 1], the slope rises right, so a peak must exist on the right. Otherwise a peak exists at mid or left.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Scan for an element greater than both neighbors. That is O(n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Search while left < right.
2. Compare nums[mid] and nums[mid + 1].
3. If rising, move left to mid + 1.
4. Otherwise move right to mid.
5. Return left.

## Dry Run

Use a small input for `Find Peak Element` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findPeakElement(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1

        while left < right:
            mid = (left + right) // 2

            if nums[mid] < nums[mid + 1]:
                left = mid + 1
            else:
                right = mid

        return left
```

## Complexity Analysis

Time O(log n), space O(1).

## Common Mistakes

- Trying to find the maximum value instead of any peak.
- Accessing mid - 1 and mid + 1 without boundary care.
- Discarding mid when it could be a peak.

## What You Should Learn

Binary search can work on local monotonic direction, not only sorted arrays.
