# 10. Product of Array Except Self

## Links

- LeetCode: [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
- Pattern: [Prefix Sum](../../patterns/prefix-sum.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

For each index, return the product of all numbers except the number at that index.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The answer at i is product of everything before i times product of everything after i. A left pass and right pass provide those pieces.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

For every index, multiply all other values. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Create an answer array initialized to 1.
2. Left pass: store product of values before each index.
3. Right pass: multiply by product of values after each index.
4. Update the running suffix after using it.
5. Return answer.

## Dry Run

Use a small input for `Product of Array Except Self` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        answer = [1] * len(nums)

        prefix = 1
        for i, value in enumerate(nums):
            answer[i] = prefix
            prefix *= value

        suffix = 1
        for i in range(len(nums) - 1, -1, -1):
            answer[i] *= suffix
            suffix *= nums[i]

        return answer
```

## Complexity Analysis

Time O(n), space O(1) extra if the output array is not counted.

## Common Mistakes

- Using division and failing with zeros.
- Multiplying nums[i] into suffix before updating answer[i].
- Allocating separate prefix and suffix arrays when one output array is enough.

## What You Should Learn

Prefix accumulation can represent any associative operation, not only addition.
