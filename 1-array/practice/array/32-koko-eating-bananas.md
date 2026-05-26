# 32. Koko Eating Bananas

## Links

- LeetCode: [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
- Pattern: [Binary Search On Answer](../../patterns/binary-search-on-answer.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the smallest eating speed that lets Koko finish all piles within h hours.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If speed s is enough, every speed greater than s is also enough. That monotonic feasibility lets us binary search speed.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every speed from 1 to max pile and simulate hours. That can be too slow.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Set low to 1 and high to max pile.
2. For a speed, compute total hours using ceiling division.
3. If hours <= h, speed works, so try smaller.
4. Otherwise try larger.
5. Return low.

## Dry Run

Use a small input for `Koko Eating Bananas` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        left, right = 1, max(piles)

        def can_finish(speed: int) -> bool:
            hours = 0
            for pile in piles:
                hours += (pile + speed - 1) // speed
            return hours <= h

        while left < right:
            mid = (left + right) // 2
            if can_finish(mid):
                right = mid
            else:
                left = mid + 1

        return left
```

## Complexity Analysis

Time O(n log max(piles)), space O(1).

## Common Mistakes

- Using normal division instead of ceiling division.
- Moving left when a speed works in a minimization problem.
- Setting high to sum(piles) unnecessarily.

## What You Should Learn

Minimum feasible value problems usually use `if works(mid): right = mid`.
