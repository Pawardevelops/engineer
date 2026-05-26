# 42. Maximum Subarray

## Links

- LeetCode: [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- Pattern: [Kadane And Subarray Optimization](../../patterns/kadane.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the largest sum of any non-empty contiguous subarray.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The best subarray ending at current value is either the value alone or the previous best-ending-here plus the value.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Compute every subarray sum and keep the maximum. That is O(n^2) with incremental sums.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Initialize current and best to nums[0].
2. For each next value, choose max(value, current + value).
3. Update best with current.
4. Never reset to 0 unless empty subarrays are allowed, which they are not.
5. Return best.

## Dry Run

Use a small input for `Maximum Subarray` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def maxSubArray(self, nums: List[int]) -> int:
        current = nums[0]
        best = nums[0]

        for value in nums[1:]:
            current = max(value, current + value)
            best = max(best, current)

        return best
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Initializing best to 0 and failing all-negative arrays.
- Thinking the answer can skip elements.
- Keeping a negative prefix when restarting is better.

## What You Should Learn

Kadane is local dynamic programming for contiguous subarray optimization.
