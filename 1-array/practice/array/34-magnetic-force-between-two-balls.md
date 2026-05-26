# 34. Magnetic Force Between Two Balls

## Links

- LeetCode: [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls/)
- Pattern: [Binary Search On Answer](../../patterns/binary-search-on-answer.md), [Sorting-Based Array Patterns](../../patterns/sorting.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Place m balls in basket positions so the minimum distance between any two balls is as large as possible.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

After sorting positions, we can greedily test whether a distance d is achievable. If d works, smaller distances also work, so try larger.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try all placements of balls and compute minimum distances. That is combinatorial.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort positions.
2. Binary search distance from 1 to max gap.
3. For a candidate distance, greedily place balls as early as possible.
4. If at least m balls fit, try a larger distance.
5. Otherwise try a smaller distance.

## Dry Run

Use a small input for `Magnetic Force Between Two Balls` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def maxDistance(self, position: List[int], m: int) -> int:
        position.sort()
        left, right = 1, position[-1] - position[0]
        best = 1

        def can_place(distance: int) -> bool:
            count = 1
            last = position[0]

            for spot in position[1:]:
                if spot - last >= distance:
                    count += 1
                    last = spot
                    if count == m:
                        return True

            return False

        while left <= right:
            mid = (left + right) // 2
            if can_place(mid):
                best = mid
                left = mid + 1
            else:
                right = mid - 1

        return best
```

## Complexity Analysis

Time O(n log n + n log range), space O(1) extra.

## Common Mistakes

- Using the minimization template and moving the wrong side.
- Not sorting positions first.
- Trying to place balls in every combination.

## What You Should Learn

Maximize-minimum problems often binary search the minimum value and greedily test feasibility.
