# 44. Maximum Sum Circular Subarray

## Links

- LeetCode: [Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/)
- Pattern: [Kadane And Subarray Optimization](../../patterns/kadane.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the maximum sum of a non-empty subarray in a circular array.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The best answer is either normal maximum subarray or a wrapped subarray. A wrapped subarray equals total sum minus the minimum subarray excluded from the middle.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Duplicate the array and check valid circular subarrays. That is more complex and can be O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Run Kadane for maximum subarray.
2. Run Kadane-style logic for minimum subarray.
3. Compute total sum.
4. If all numbers are negative, return max_sum.
5. Otherwise return max(max_sum, total - min_sum).

## Dry Run

Use a small input for `Maximum Sum Circular Subarray` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def maxSubarraySumCircular(self, nums: List[int]) -> int:
        total = sum(nums)

        max_current = max_sum = nums[0]
        min_current = min_sum = nums[0]

        for value in nums[1:]:
            max_current = max(value, max_current + value)
            max_sum = max(max_sum, max_current)

            min_current = min(value, min_current + value)
            min_sum = min(min_sum, min_current)

        if max_sum < 0:
            return max_sum

        return max(max_sum, total - min_sum)
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Returning 0 for all-negative arrays.
- Forgetting that wrapped answer excludes a minimum subarray.
- Allowing the minimum subarray to be the whole array.

## What You Should Learn

Circular max subarray can be transformed into total minus a minimum subarray.
