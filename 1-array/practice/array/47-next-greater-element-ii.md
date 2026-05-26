# 47. Next Greater Element II

## Links

- LeetCode: [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)
- Pattern: [Monotonic Stack](../../patterns/monotonic-stack.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

For each value in a circular array, find the next greater value when moving right and wrapping around.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A decreasing stack tracks unresolved indexes. Scanning 2n positions lets indexes near the end see values at the beginning.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

For each index, check up to n - 1 next positions. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Initialize answers to -1.
2. Loop i from 0 to 2n - 1.
3. Use index i % n.
4. Pop indexes whose value is smaller than current value and set their answer.
5. Only push indexes during the first pass.

## Dry Run

Use a small input for `Next Greater Element II` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        n = len(nums)
        answer = [-1] * n
        stack = []

        for i in range(2 * n):
            index = i % n

            while stack and nums[stack[-1]] < nums[index]:
                prev = stack.pop()
                answer[prev] = nums[index]

            if i < n:
                stack.append(index)

        return answer
```

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Pushing indexes during both passes.
- Returning indexes instead of values.
- Forgetting modulo for circular access.

## What You Should Learn

Circular next-greater problems can usually be handled by scanning twice while only adding original indexes once.
