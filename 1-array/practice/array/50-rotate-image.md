# 50. Rotate Image

## Links

- LeetCode: [Rotate Image](https://leetcode.com/problems/rotate-image/)
- Pattern: [Matrix Array Problems](../../patterns/matrix.md), [In-Place Array Techniques](../../patterns/in-place-array-techniques.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Rotate an n x n matrix 90 degrees clockwise in-place.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A clockwise rotation equals transpose across the main diagonal followed by reversing each row.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Create a new matrix and copy each value to its rotated position. That uses O(n^2) extra space.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Transpose the matrix by swapping matrix[row][col] with matrix[col][row] for col > row.
2. Reverse every row.
3. Do both operations in-place.
4. Return nothing because the matrix is modified directly.
5. Use square matrix size n.

## Dry Run

Use a small input for `Rotate Image` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)

        for row in range(n):
            for col in range(row + 1, n):
                matrix[row][col], matrix[col][row] = matrix[col][row], matrix[row][col]

        for row in matrix:
            row.reverse()
```

## Complexity Analysis

Time O(n^2), space O(1).

## Common Mistakes

- Swapping every pair twice during transpose.
- Reversing columns instead of rows for clockwise rotation.
- Allocating a second matrix when in-place is required.

## What You Should Learn

Many matrix rotations are combinations of transpose and reverse.
