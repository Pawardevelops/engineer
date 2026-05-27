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

## Visual Explanation

Example:

```text
piles = [3, 6, 7, 11]
h = 8
```

Possible eating speeds:

```text
speed:  1   2   3   4   5   6   7   8   9   10   11
works:  F   F   F   T   T   T   T   T   T    T    T
                    ^
              minimum speed
```

This true/false shape is why binary search works.

For speed `4`:

```text
pile 3  -> ceil(3 / 4)  = 1 hour
pile 6  -> ceil(6 / 4)  = 2 hours
pile 7  -> ceil(7 / 4)  = 2 hours
pile 11 -> ceil(11 / 4) = 3 hours
total = 8 hours
```

Speed `4` works, so we try smaller speeds.

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

Input:

```text
piles = [3, 6, 7, 11]
h = 8
```

| Step | left | right | mid speed | hours needed | Works? | Decision |
|---|---:|---:|---:|---:|---|---|
| 1 | 1 | 11 | 6 | 6 | Yes | Try smaller, right = 6. |
| 2 | 1 | 6 | 3 | 10 | No | Need faster, left = 4. |
| 3 | 4 | 6 | 5 | 8 | Yes | Try smaller, right = 5. |
| 4 | 4 | 5 | 4 | 8 | Yes | Try smaller, right = 4. |

Now `left == right == 4`, so answer is `4`.

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

## Line-By-Line Explanation

```text
left, right = 1, max(piles)
```

The slowest possible speed is 1. The fastest speed we need to consider is the largest pile.

```text
hours += (pile + speed - 1) // speed
```

This is integer ceiling division. It calculates how many full hours are needed for one pile.

```text
if can_finish(mid):
    right = mid
```

If speed `mid` works, it might be the answer, so keep it and search smaller speeds.

```text
else:
    left = mid + 1
```

If speed `mid` does not work, every slower speed also fails.

## Complexity Analysis

Time O(n log max(piles)), space O(1).

## Common Mistakes

- Using normal division instead of ceiling division.
- Moving left when a speed works in a minimization problem.
- Setting high to sum(piles) unnecessarily.

## What You Should Learn

Minimum feasible value problems usually use `if works(mid): right = mid`.
