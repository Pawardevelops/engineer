# 17. Max Consecutive Ones III

## Links

- LeetCode: [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)
- Pattern: [Sliding Window](../../patterns/sliding-window.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the longest subarray containing only 1s after flipping at most k zeros.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A window is valid if it contains at most k zeros. The values inside do not need to be changed; only the zero count matters.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every start and count zeros until more than k appear. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Expand right.
2. Increase zero count when nums[right] is 0.
3. Shrink left while zero count exceeds k.
4. After restoring validity, update best length.
5. Return best.

## Dry Run

Use a small input for `Max Consecutive Ones III` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def longestOnes(self, nums: List[int], k: int) -> int:
        left = 0
        zeros = 0
        best = 0

        for right, value in enumerate(nums):
            if value == 0:
                zeros += 1

            while zeros > k:
                if nums[left] == 0:
                    zeros -= 1
                left += 1

            best = max(best, right - left + 1)

        return best
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Actually modifying the array.
- Shrinking when zeros == k instead of zeros > k.
- Counting ones instead of tracking the limiting zeros.

## What You Should Learn

Many replacement problems are really longest window with at most k invalid elements.
