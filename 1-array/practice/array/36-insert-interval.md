# 36. Insert Interval

## Links

- LeetCode: [Insert Interval](https://leetcode.com/problems/insert-interval/)
- Pattern: [Intervals](../../patterns/intervals.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Insert a new interval into a sorted non-overlapping interval list and merge if needed.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Intervals before the new interval can be copied, overlapping intervals are merged into the new interval, and intervals after can be copied.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Append the new interval, sort, then run merge intervals. That works but ignores the sorted non-overlapping input.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Copy intervals that end before the new interval starts.
2. Merge all intervals that overlap the new interval.
3. Append the merged new interval.
4. Copy the remaining intervals.
5. Return result.

## Dry Run

Use a small input for `Insert Interval` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        result = []
        i = 0
        n = len(intervals)

        while i < n and intervals[i][1] < newInterval[0]:
            result.append(intervals[i])
            i += 1

        while i < n and intervals[i][0] <= newInterval[1]:
            newInterval[0] = min(newInterval[0], intervals[i][0])
            newInterval[1] = max(newInterval[1], intervals[i][1])
            i += 1

        result.append(newInterval)

        while i < n:
            result.append(intervals[i])
            i += 1

        return result
```

## Complexity Analysis

Time O(n), space O(n) for output.

## Common Mistakes

- Sorting unnecessarily.
- Using non-overlap conditions backwards.
- Forgetting to append the merged new interval.

## What You Should Learn

Many interval tasks split naturally into before, overlapping, and after phases.
