# 08. Next Permutation

## Links

- LeetCode: [Next Permutation](https://leetcode.com/problems/next-permutation/)
- Pattern: [In-Place Array Techniques](../../patterns/in-place-array-techniques.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Transform the array into the next lexicographically larger permutation, or the smallest permutation if no larger one exists.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The rightmost decreasing suffix is already the largest arrangement for that suffix. The pivot just before it is the position that must be minimally increased.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Generate all permutations, sort them, and pick the next. That is not practical.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Scan from the right to find the first index i where nums[i] < nums[i + 1].
2. If no pivot exists, reverse the whole array.
3. Scan from the right to find the smallest value greater than nums[i].
4. Swap pivot with that value.
5. Reverse the suffix after i to make it as small as possible.

## Dry Run

Use a small input for `Next Permutation` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def nextPermutation(self, nums: List[int]) -> None:
        i = len(nums) - 2
        while i >= 0 and nums[i] >= nums[i + 1]:
            i -= 1

        if i >= 0:
            j = len(nums) - 1
            while nums[j] <= nums[i]:
                j -= 1
            nums[i], nums[j] = nums[j], nums[i]

        left, right = i + 1, len(nums) - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Choosing the leftmost pivot instead of the rightmost pivot.
- Sorting the suffix instead of reversing it after recognizing it is descending.
- Forgetting the all-descending case.

## What You Should Learn

Lexicographic next-step problems are solved by changing the rightmost possible position and minimizing everything after it.
