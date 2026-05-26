# 09. Rotate Array

## Links

- LeetCode: [Rotate Array](https://leetcode.com/problems/rotate-array/)
- Pattern: [In-Place Array Techniques](../../patterns/in-place-array-techniques.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Move every element k positions to the right, wrapping around the end.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A right rotation can be decomposed into three reversals: reverse all, reverse the first k, then reverse the remaining elements.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Create a new array and place each value at its rotated index. That is clear but uses O(n) space.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Reduce k with k %= n.
2. Reverse the whole array.
3. Reverse indexes 0 through k - 1.
4. Reverse indexes k through n - 1.
5. The array is now rotated in-place.

## Dry Run

Use a small input for `Rotate Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def rotate(self, nums: List[int], k: int) -> None:
        n = len(nums)
        k %= n

        def reverse(left: int, right: int) -> None:
            while left < right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1

        reverse(0, n - 1)
        reverse(0, k - 1)
        reverse(k, n - 1)
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Forgetting k %= n.
- Mixing left rotation and right rotation reversal order.
- Creating extra memory when the problem asks for in-place.

## What You Should Learn

Some array transformations become simple when viewed as reversals of meaningful segments.
