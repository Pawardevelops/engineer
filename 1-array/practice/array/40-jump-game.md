# 40. Jump Game

## Links

- LeetCode: [Jump Game](https://leetcode.com/problems/jump-game/)
- Pattern: [Greedy Array Decisions](../../patterns/greedy-arrays.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Determine whether you can reach the last index when each value is the maximum jump length from that position.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If the current index is reachable, only the farthest reachable index matters. Any smaller reach is dominated.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try all jump paths recursively or with DP. That can explore many redundant states.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Set farthest to 0.
2. Scan indexes.
3. If i is greater than farthest, return false.
4. Update farthest with i + nums[i].
5. If scan completes, return true.

## Dry Run

Use a small input for `Jump Game` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def canJump(self, nums: List[int]) -> bool:
        farthest = 0

        for i, jump in enumerate(nums):
            if i > farthest:
                return False
            farthest = max(farthest, i + jump)

        return True
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Choosing the locally longest jump path instead of tracking farthest reach.
- Ignoring unreachable indexes.
- Using recursion and hitting exponential behavior.

## What You Should Learn

Reachability can often be summarized by the farthest boundary reached so far.
