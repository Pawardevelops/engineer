# 18. Minimum Operations to Reduce X to Zero

## Links

- LeetCode: [Minimum Operations to Reduce X to Zero](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/)
- Pattern: [Sliding Window](../../patterns/sliding-window.md), [Prefix Sum](../../patterns/prefix-sum.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Remove numbers from the left or right end until the removed sum is x, using the fewest removals.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Keeping a middle subarray of sum total - x is equivalent to removing the ends. Since values are positive, sliding window finds the longest such middle subarray.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every number of removals from the left and right. That repeats many sums.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Compute target = total sum - x.
2. If target is 0, all elements must be removed.
3. Find the longest subarray with sum target using sliding window.
4. Answer is n - longest length.
5. If no such subarray exists, return -1.

## Dry Run

Use a small input for `Minimum Operations to Reduce X to Zero` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def minOperations(self, nums: List[int], x: int) -> int:
        target = sum(nums) - x
        if target < 0:
            return -1
        if target == 0:
            return len(nums)

        left = 0
        current = 0
        longest = -1

        for right, value in enumerate(nums):
            current += value

            while current > target:
                current -= nums[left]
                left += 1

            if current == target:
                longest = max(longest, right - left + 1)

        return -1 if longest == -1 else len(nums) - longest
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Trying to greedily remove the larger end.
- Looking for shortest removed ends directly instead of longest kept middle.
- Forgetting target can be negative or zero.

## What You Should Learn

The right transformation can turn a hard-looking end-removal problem into a standard subarray problem.
