# 01. Container With Most Water

## Links

- LeetCode: [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- Pattern: [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Given heights of vertical lines, choose two lines that hold the most water with the x-axis. The area is width times the shorter height.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The two outermost lines give maximum width first. Since area is limited by the shorter line, moving the taller line inward only loses width without improving the limiting height.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every pair of lines and compute its area. That proves the answer definition clearly, but it checks O(n^2) pairs.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Start left at 0 and right at n - 1.
2. Compute area using the current width and shorter height.
3. Update the best area.
4. Move the pointer at the shorter height because that is the bottleneck.
5. Stop when the pointers meet.

## Dry Run

Use a small input for `Container With Most Water` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        best = 0

        while left < right:
            width = right - left
            best = max(best, width * min(height[left], height[right]))

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return best
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Moving the taller pointer.
- Forgetting width is right - left.
- Stopping after one local increase instead of scanning until pointers meet.

## What You Should Learn

You learn how a pointer move can be justified by eliminating dominated choices.
