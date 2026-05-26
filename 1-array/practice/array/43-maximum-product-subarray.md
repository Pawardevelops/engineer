# 43. Maximum Product Subarray

## Links

- LeetCode: [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
- Pattern: [Kadane And Subarray Optimization](../../patterns/kadane.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the largest product of any non-empty contiguous subarray.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A negative value can turn the smallest product into the largest. Therefore we track both max-ending-here and min-ending-here.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every subarray product. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Initialize max_here, min_here, and best to nums[0].
2. For each value, if it is negative, swap max_here and min_here.
3. Update max_here as max(value, max_here * value).
4. Update min_here as min(value, min_here * value).
5. Update best.

## Dry Run

Use a small input for `Maximum Product Subarray` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def maxProduct(self, nums: List[int]) -> int:
        max_here = nums[0]
        min_here = nums[0]
        best = nums[0]

        for value in nums[1:]:
            if value < 0:
                max_here, min_here = min_here, max_here

            max_here = max(value, max_here * value)
            min_here = min(value, min_here * value)
            best = max(best, max_here)

        return best
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Tracking only max_here.
- Not handling zero as a natural restart.
- Swapping after updating instead of before for negative values.

## What You Should Learn

When signs can flip, the worst current state may become the best future state.
