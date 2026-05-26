# 25. H-Index

## Links

- LeetCode: [H-Index](https://leetcode.com/problems/h-index/)
- Pattern: [Sorting-Based Array Patterns](../../patterns/sorting.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the largest h such that at least h papers have at least h citations each.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Sorting descending lets index i represent how many papers have been seen with citation counts at least as large as the current one.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try every possible h and count papers with citations >= h. That is O(n^2) if done naively.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Sort citations descending.
2. Scan with 1-based paper count.
3. If citations at this position is at least the count, update h.
4. Stop when the condition fails.
5. Return h.

## Dry Run

Use a small input for `H-Index` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def hIndex(self, citations: List[int]) -> int:
        citations.sort(reverse=True)
        h = 0

        for papers, citation_count in enumerate(citations, 1):
            if citation_count >= papers:
                h = papers
            else:
                break

        return h
```

## Complexity Analysis

Time O(n log n), space O(1) extra depending on sort implementation.

## Common Mistakes

- Using 0-based index directly as paper count.
- Returning citation_count instead of h.
- Stopping before updating h for a valid position.

## What You Should Learn

Definitions involving counts often become easier after sorting into a meaningful order.
