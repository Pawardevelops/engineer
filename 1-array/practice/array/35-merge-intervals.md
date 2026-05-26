# 35. Merge Intervals

## Links

- LeetCode: [Merge Intervals](https://leetcode.com/problems/merge-intervals/)
- Pattern: [Intervals](../../patterns/intervals.md), [Sorting-Based Array Patterns](../../patterns/sorting.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Combine all overlapping intervals and return the non-overlapping merged result.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

After sorting by start, if the next interval overlaps the last merged interval, they must belong together. Otherwise it starts a new merged interval.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Repeatedly compare every interval with every other interval and merge until stable. That is complex and slow.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort intervals by start.
2. Iterate through intervals.
3. If merged is empty or current start is after last end, append it.
4. Otherwise extend last end.
5. Return merged.

## Dry Run

Use a small input for `Merge Intervals` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda interval: interval[0])
        merged = []

        for start, end in intervals:
            if not merged or start > merged[-1][1]:
                merged.append([start, end])
            else:
                merged[-1][1] = max(merged[-1][1], end)

        return merged
```

## Complexity Analysis

Time O(n log n), space O(n) for output.

## Common Mistakes

- Not sorting first.
- Using start >= last_end when touching intervals should merge for this problem.
- Appending the current interval before deciding overlap.

## What You Should Learn

Sorting intervals changes overlap detection from many-to-many into neighbor comparisons.
