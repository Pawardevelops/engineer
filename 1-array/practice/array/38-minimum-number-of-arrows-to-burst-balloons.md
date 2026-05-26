# 38. Minimum Number of Arrows to Burst Balloons

## Links

- LeetCode: [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)
- Pattern: [Intervals](../../patterns/intervals.md), [Greedy Array Decisions](../../patterns/greedy-arrays.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Each balloon spans an interval. Find the minimum arrows needed where one arrow at position x bursts every interval containing x.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Sorting by end lets us shoot at the earliest possible end. That arrow covers all intervals starting before or at that end.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try many arrow positions or combinations. The continuous coordinate range makes that impractical.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort points by end.
2. Shoot the first arrow at the first end.
3. For each interval, if its start is greater than arrow position, need a new arrow.
4. Place the new arrow at this interval's end.
5. Return arrow count.

## Dry Run

Use a small input for `Minimum Number of Arrows to Burst Balloons` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points.sort(key=lambda point: point[1])
        arrows = 1
        arrow_at = points[0][1]

        for start, end in points[1:]:
            if start > arrow_at:
                arrows += 1
                arrow_at = end

        return arrows
```

## Complexity Analysis

Time O(n log n), space O(1) extra depending on sort.

## Common Mistakes

- Using start >= arrow_at, which wrongly separates touching intervals.
- Sorting by start and choosing unstable arrow positions.
- Forgetting there is at least one arrow when points is non-empty.

## What You Should Learn

A point covering interval problem often becomes choose earliest ending point.
