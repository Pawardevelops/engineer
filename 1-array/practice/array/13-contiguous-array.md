# 13. Contiguous Array

## Links

- LeetCode: [Contiguous Array](https://leetcode.com/problems/contiguous-array/)
- Pattern: [Prefix Sum](../../patterns/prefix-sum.md), [Hashing With Arrays](../../patterns/hashing.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the longest contiguous subarray with the same number of 0s and 1s.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Treat 0 as -1 and 1 as +1. A subarray has equal zeros and ones when the balance at its end equals a previous balance.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Check all subarrays and count zeros and ones. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Set balance 0 first seen at index -1.
2. Add +1 for 1 and -1 for 0.
3. If balance was seen, update best with the distance.
4. If balance is new, store its first index.
5. Return best length.

## Dry Run

Use a small input for `Contiguous Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findMaxLength(self, nums: List[int]) -> int:
        first_index = {0: -1}
        balance = 0
        best = 0

        for i, value in enumerate(nums):
            balance += 1 if value == 1 else -1

            if balance in first_index:
                best = max(best, i - first_index[balance])
            else:
                first_index[balance] = i

        return best
```

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Counting zeros and ones separately for every window.
- Overwriting the first index for a balance.
- Forgetting the initial balance at index -1.

## What You Should Learn

Balance transformations are a powerful way to make equality conditions numeric.
