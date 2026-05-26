# 04. 3Sum Closest

## Links

- LeetCode: [3Sum Closest](https://leetcode.com/problems/3sum-closest/)
- Pattern: [Sorting-Based Array Patterns](../../patterns/sorting.md), [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the triplet sum closest to the target.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Sorting makes the pair sum move predictably. If the current sum is below target, increasing left is the useful direction; if above, decreasing right is useful.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Compute every triplet sum and keep the closest. That is O(n^3).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort nums.
2. Initialize best with any valid triplet sum.
3. Fix i and scan left/right.
4. Update best when current sum is closer.
5. Move the pointer that can move the sum toward target.

## Dry Run

Use a small input for `3Sum Closest` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        best = nums[0] + nums[1] + nums[2]

        for i in range(len(nums) - 2):
            left, right = i + 1, len(nums) - 1

            while left < right:
                total = nums[i] + nums[left] + nums[right]

                if abs(total - target) < abs(best - target):
                    best = total

                if total < target:
                    left += 1
                elif total > target:
                    right -= 1
                else:
                    return target

        return best
```

## Complexity Analysis

Time O(n^2), space O(1) extra.

## Common Mistakes

- Initializing best to 0 instead of a real triplet.
- Moving both pointers when only one direction is justified.
- Ignoring exact match as an immediate best possible answer.

## What You Should Learn

Two-pointer movement can optimize closest-value problems, not only exact-match problems.
