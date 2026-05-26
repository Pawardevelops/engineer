# 48. Spiral Matrix

## Links

- LeetCode: [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
- Pattern: [Matrix Array Problems](../../patterns/matrix.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return all matrix elements in spiral order.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Four boundaries describe the unvisited rectangle. After traversing one side, that boundary moves inward.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Use a visited set and direction simulation. That works but adds extra state.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Initialize top, bottom, left, and right boundaries.
2. Traverse top row, then increment top.
3. Traverse right column, then decrement right.
4. If rows remain, traverse bottom row.
5. If columns remain, traverse left column.

## Dry Run

Use a small input for `Spiral Matrix` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result = []
        top, bottom = 0, len(matrix) - 1
        left, right = 0, len(matrix[0]) - 1

        while top <= bottom and left <= right:
            for col in range(left, right + 1):
                result.append(matrix[top][col])
            top += 1

            for row in range(top, bottom + 1):
                result.append(matrix[row][right])
            right -= 1

            if top <= bottom:
                for col in range(right, left - 1, -1):
                    result.append(matrix[bottom][col])
                bottom -= 1

            if left <= right:
                for row in range(bottom, top - 1, -1):
                    result.append(matrix[row][left])
                left += 1

        return result
```

## Complexity Analysis

Time O(mn), space O(1) extra besides output.

## Common Mistakes

- Forgetting the checks before bottom row and left column.
- Moving boundaries before reading their side.
- Using matrix[0] without ensuring the matrix is non-empty in a generic version.

## What You Should Learn

Matrix traversal is mostly about preserving boundary invariants.
