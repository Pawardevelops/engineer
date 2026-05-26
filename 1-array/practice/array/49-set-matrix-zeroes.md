# 49. Set Matrix Zeroes

## Links

- LeetCode: [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)
- Pattern: [Matrix Array Problems](../../patterns/matrix.md), [In-Place Array Techniques](../../patterns/in-place-array-techniques.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

If a cell is zero, set its entire row and column to zero in-place.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The first row and first column can store which rows and columns need zeroing. Separate flags protect whether those marker areas originally needed zeroing.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Store all zero rows and columns in sets, then zero them. That uses O(m + n) space.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Check whether first row and first column originally contain zero.
2. Use matrix[row][0] and matrix[0][col] as markers for other cells.
3. Zero marked inner cells.
4. Zero first row if needed.
5. Zero first column if needed.

## Dry Run

Use a small input for `Set Matrix Zeroes` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def setZeroes(self, matrix: List[List[int]]) -> None:
        rows, cols = len(matrix), len(matrix[0])
        first_row_zero = any(matrix[0][col] == 0 for col in range(cols))
        first_col_zero = any(matrix[row][0] == 0 for row in range(rows))

        for row in range(1, rows):
            for col in range(1, cols):
                if matrix[row][col] == 0:
                    matrix[row][0] = 0
                    matrix[0][col] = 0

        for row in range(1, rows):
            for col in range(1, cols):
                if matrix[row][0] == 0 or matrix[0][col] == 0:
                    matrix[row][col] = 0

        if first_row_zero:
            for col in range(cols):
                matrix[0][col] = 0

        if first_col_zero:
            for row in range(rows):
                matrix[row][0] = 0
```

## Complexity Analysis

Time O(mn), space O(1).

## Common Mistakes

- Zeroing rows immediately and destroying marker information.
- Forgetting separate first-row and first-column flags.
- Starting marker loops at 0 and corrupting markers.

## What You Should Learn

In-place matrix problems often reserve part of the matrix as metadata.
