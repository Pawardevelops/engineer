# 33. Capacity To Ship Packages Within D Days

## Links

- LeetCode: [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
- Pattern: [Binary Search On Answer](../../patterns/binary-search-on-answer.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the minimum ship capacity needed to ship packages in order within a given number of days.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If capacity c works, every larger capacity also works. The feasibility check counts how many days are needed for a candidate capacity.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try capacities one by one from max package to total weight. That can be huge.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Low is max(weights), because every package must fit.
2. High is sum(weights), capacity for one day.
3. Simulate days for mid capacity.
4. If days needed <= limit, try smaller capacity.
5. Otherwise increase capacity.

## Dry Run

Use a small input for `Capacity To Ship Packages Within D Days` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        left, right = max(weights), sum(weights)

        def can_ship(capacity: int) -> bool:
            used_days = 1
            current = 0

            for weight in weights:
                if current + weight > capacity:
                    used_days += 1
                    current = 0
                current += weight

            return used_days <= days

        while left < right:
            mid = (left + right) // 2
            if can_ship(mid):
                right = mid
            else:
                left = mid + 1

        return left
```

## Complexity Analysis

Time O(n log sum(weights)), space O(1).

## Common Mistakes

- Starting low at 1 instead of max weight.
- Reordering packages even though order must stay fixed.
- Counting a new day after adding an overweight package instead of before.

## What You Should Learn

Good binary-search-on-answer solutions depend on strong low/high bounds and a faithful feasibility check.
