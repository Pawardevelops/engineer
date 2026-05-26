# 41. Jump Game II

## Links

- LeetCode: [Jump Game II](https://leetcode.com/problems/jump-game-ii/)
- Pattern: [Greedy Array Decisions](../../patterns/greedy-arrays.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the minimum number of jumps needed to reach the last index.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

All indexes within current_end are reachable with the current number of jumps. While scanning that layer, farthest records the next layer boundary.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Use BFS or DP over all reachable jumps. That can be O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Track jumps, current_end, and farthest.
2. Scan until the second-last index.
3. Update farthest from each position.
4. When i reaches current_end, take one jump and move current_end to farthest.
5. Return jumps.

## Dry Run

Use a small input for `Jump Game II` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def jump(self, nums: List[int]) -> int:
        jumps = 0
        current_end = 0
        farthest = 0

        for i in range(len(nums) - 1):
            farthest = max(farthest, i + nums[i])

            if i == current_end:
                jumps += 1
                current_end = farthest

        return jumps
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Looping through the last index and adding an extra jump.
- Jumping immediately to the locally farthest index instead of finishing the layer.
- Confusing current_end with farthest.

## What You Should Learn

Minimum jumps can be viewed as BFS layers compressed into a greedy scan.
