# 19. Longest Consecutive Sequence

## Links

- LeetCode: [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
- Pattern: [Hashing With Arrays](../../patterns/hashing.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the length of the longest run of consecutive integer values, regardless of their original order.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A set gives O(1)-average membership checks. Starting only at numbers with no predecessor prevents repeated sequence walks.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

For every value, repeatedly search for value + 1 in the original array. That can become O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Put all numbers in a set.
2. For each value, only start counting if value - 1 is absent.
3. Walk forward while value + length exists.
4. Update best.
5. Return best.

## Dry Run

Use a small input for `Longest Consecutive Sequence` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def longestConsecutive(self, nums: List[int]) -> int:
        values = set(nums)
        best = 0

        for value in values:
            if value - 1 in values:
                continue

            length = 1
            while value + length in values:
                length += 1

            best = max(best, length)

        return best
```

## Complexity Analysis

Time O(n) average, space O(n).

## Common Mistakes

- Starting a walk from every number.
- Sorting when the expected solution is O(n).
- Looping over nums and being confused by duplicates; looping over the set is cleaner.

## What You Should Learn

The start-of-sequence test is the whole optimization.
