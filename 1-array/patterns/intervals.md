# Intervals

## Core Idea

Treat each item as a range with a start and end. Sort ranges so overlaps and gaps become local decisions.

## Visual Mental Model

Intervals are not single values. They cover space.

```text
[1, 4]      covers 1----4
[2, 6]      covers   2------6
[8, 10]     covers          8--10

[1, 4] and [2, 6] overlap because 2 <= 4.
```

After sorting by start:

```text
[1, 4], [2, 6], [8, 10]
   current next

If next.start <= current.end:
merge them.
```

## Why This Pattern Exists

Intervals look like pairs of numbers, but the important relationship is geometric: ranges can overlap, touch, contain each other, or stay separate.

The pattern is useful because it gives you a repeatable way to answer this question:

```text
What information do I keep so I do not repeat work?
```

For array problems, the repeated work is usually one of these:

- Checking the same pair or range again
- Recomputing a subarray property from the beginning
- Searching for a value that could have been remembered
- Revisiting cells, intervals, or candidates that can already be ruled out

## When To Use It

- Each element is [start, end].
- The problem asks to merge, insert, erase, cover, or count overlaps.
- Sorting by start or end creates a greedy order.
- The answer depends on overlap relationships, not individual points.

## When Not To Use It

- The array values are independent numbers, not ranges.
- The problem needs every point inside every interval explicitly.
- A sweep-line event solution is required for many simultaneous starts and ends.

## Common Shapes

### Merge by start
Sort by start and extend the current interval while overlaps continue.

### Erase by end
Sort by end and keep the interval that leaves most room for future intervals.

### Cover by end
Use one arrow or resource until the next interval starts after the current end.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def merge_intervals(intervals: List[List[int]]) -> List[List[int]]:
    intervals.sort(key=lambda interval: interval[0])
    merged = []

    for start, end in intervals:
        if not merged or start > merged[-1][1]:
            merged.append([start, end])
        else:
            merged[-1][1] = max(merged[-1][1], end)

    return merged
```

## Worked Mini Examples

### Merge intervals
Overlapping neighbors after sorting belong to the same merged range.

### Insert interval
Copy before, merge overlaps with the new interval, then copy after.

### Minimum arrows
One arrow at the smallest current end bursts all overlapping balloons.

## Three Warm-Up Drills

| No. | Drill | Why It Helps |
|---|---|---|
| 1 | [Summary Ranges](https://leetcode.com/problems/summary-ranges/) | Converts consecutive numbers into ranges. |
| 2 | [Merge Intervals](https://leetcode.com/problems/merge-intervals/) | The core interval merge pattern. |
| 3 | [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) | Greedy interval coverage. |

## Study Links

- [NeetCode Practice](https://neetcode.io/practice)
- [LeetCode 75](https://leetcode.com/studyplan/leetcode-75/)

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Sorting by the wrong endpoint for the chosen greedy strategy.
- Using `<` instead of `<=` when touching intervals should merge.
- Mutating an input interval that will be needed unchanged elsewhere.

## Questions Using This Pattern

- [35. Merge Intervals](../practice/array/35-merge-intervals.md)
- [36. Insert Interval](../practice/array/36-insert-interval.md)
- [37. Non-overlapping Intervals](../practice/array/37-non-overlapping-intervals.md)
- [38. Minimum Number of Arrows to Burst Balloons](../practice/array/38-minimum-number-of-arrows-to-burst-balloons.md)
