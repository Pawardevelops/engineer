# 37. Non-overlapping Intervals

## Links

- LeetCode: [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
- Pattern: [Intervals](../../patterns/intervals.md), [Greedy Array Decisions](../../patterns/greedy-arrays.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return the minimum number of intervals to remove so the rest do not overlap.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Keeping the interval with the earliest end leaves maximum room for future intervals. Sorting by end makes this greedy choice local.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try all subsets of intervals and choose the largest non-overlapping set. That is exponential.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort intervals by end.
2. Keep the end of the last selected interval.
3. If current start is before last end, remove it.
4. Otherwise keep it and update last end.
5. Return removals.

## Dry Run

Use a small input for `Non-overlapping Intervals` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key=lambda interval: interval[1])
        removals = 0
        last_end = intervals[0][1]

        for start, end in intervals[1:]:
            if start < last_end:
                removals += 1
            else:
                last_end = end

        return removals
```

## Complexity Analysis

Time O(n log n), space O(1) extra depending on sort.

## Common Mistakes

- Sorting by start and keeping long intervals that block many future intervals.
- Treating touching intervals as overlapping.
- Updating last_end when removing the current interval.

## What You Should Learn

Greedy interval selection usually favors the earliest finishing interval.
