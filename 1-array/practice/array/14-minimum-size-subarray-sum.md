# 14. Minimum Size Subarray Sum

## Links

- LeetCode: [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
- Pattern: [Sliding Window](../../patterns/sliding-window.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the minimum length of a contiguous subarray whose sum is at least target.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

All numbers are positive, so expanding right never decreases the sum and moving left never increases it. That monotonic behavior makes sliding window valid.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every start and grow every end until target is reached. This can still be O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Move right across the array while adding values to the sum.
2. When sum is at least target, update the best length.
3. Shrink from the left to see if a shorter valid window exists.
4. Repeat until the right side finishes.
5. Return 0 if no valid window was found.

## Dry Run

Use a small input for `Minimum Size Subarray Sum` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        current = 0
        best = len(nums) + 1

        for right, value in enumerate(nums):
            current += value

            while current >= target:
                best = min(best, right - left + 1)
                current -= nums[left]
                left += 1

        return 0 if best == len(nums) + 1 else best
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Using this exact window logic when negatives are present.
- Shrinking only once instead of while valid.
- Returning a sentinel length instead of 0 when no answer exists.

## What You Should Learn

For minimum valid windows, update the answer before each shrink.
