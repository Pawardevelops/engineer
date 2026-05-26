# 12. Continuous Subarray Sum

## Links

- LeetCode: [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/)
- Pattern: [Prefix Sum](../../patterns/prefix-sum.md), [Hashing With Arrays](../../patterns/hashing.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Check whether there is a subarray of length at least two whose sum is a multiple of k.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If two prefix sums have the same remainder modulo k, their difference is divisible by k. The distance between indexes gives the length.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Check every subarray sum and test divisibility. That takes O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Store first occurrence of each remainder.
2. Seed remainder 0 at index -1.
3. Update running prefix modulo k.
4. If the same remainder was seen and the distance is at least 2, return true.
5. Only store the first index for each remainder.

## Dry Run

Use a small input for `Continuous Subarray Sum` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        first_index = {0: -1}
        prefix = 0

        for i, value in enumerate(nums):
            prefix = (prefix + value) % k

            if prefix in first_index:
                if i - first_index[prefix] >= 2:
                    return True
            else:
                first_index[prefix] = i

        return False
```

## Complexity Analysis

Time O(n), space O(min(n, k)) for positive k.

## Common Mistakes

- Updating the stored index every time and losing the longest distance.
- Forgetting the length at least two rule.
- Not seeding remainder 0 at -1.

## What You Should Learn

Modulo converts divisible subarray problems into repeated-state problems.
