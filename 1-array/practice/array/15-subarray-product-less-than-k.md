# 15. Subarray Product Less Than K

## Links

- LeetCode: [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)
- Pattern: [Sliding Window](../../patterns/sliding-window.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Count contiguous subarrays whose product is less than k.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

With positive numbers, the product grows when expanding and shrinks when removing from the left. That makes the valid window monotonic.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Multiply every subarray and count valid ones. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. If k <= 1, return 0 because all values are positive.
2. Expand right and multiply into product.
3. While product is too large, divide out nums[left].
4. All subarrays ending at right and starting from left to right are valid.
5. Add right - left + 1 to the count.

## Dry Run

Use a small input for `Subarray Product Less Than K` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1:
            return 0

        product = 1
        left = 0
        count = 0

        for right, value in enumerate(nums):
            product *= value

            while product >= k:
                product //= nums[left]
                left += 1

            count += right - left + 1

        return count
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Forgetting k <= 1.
- Counting only one subarray per right endpoint.
- Using this logic with zeros or negatives without rethinking the invariant.

## What You Should Learn

When a full window is valid, every suffix of that window ending at right is also valid.
