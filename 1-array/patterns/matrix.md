# Matrix Array Problems

## Core Idea

Treat a 2D array as rows, columns, boundaries, or a flattened 1D index depending on the structure.

## Why This Pattern Exists

Matrix problems are still array problems, but the main difficulty is controlling movement and avoiding overwritten information.

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

- The input is a list of lists.
- The problem asks for traversal, in-place update, rotation, or search.
- Rows or columns have sorted properties.
- Boundary management is more important than complex data structures.

## When Not To Use It

- The matrix represents a graph with arbitrary movement rules, where BFS/DFS is the main pattern.
- You need advanced linear algebra operations.
- The prompt allows flattening but the sorted property does not support it.

## Common Shapes

### Boundary traversal
Move top, right, bottom, left boundaries inward.

### In-place marking
Use first row and first column as storage for row/column flags.

### Flattened binary search
Map index mid to row mid // cols and col mid % cols.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def search_flat_matrix(matrix: List[List[int]], target: int) -> bool:
    rows, cols = len(matrix), len(matrix[0])
    left, right = 0, rows * cols - 1

    while left <= right:
        mid = (left + right) // 2
        value = matrix[mid // cols][mid % cols]
        if value == target:
            return True
        if value < target:
            left = mid + 1
        else:
            right = mid - 1

    return False
```

## Worked Mini Examples

### Spiral matrix
Boundaries prevent revisiting cells while walking layers.

### Set matrix zeroes
First row and first column store which rows/columns must become zero.

### Rotate image
Transpose then reverse each row to rotate clockwise.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Reading matrix[0] when the matrix may be empty.
- Overwriting marker information before it has been used.
- Missing the final row or column in boundary traversal.

## Questions Using This Pattern

- [48. Spiral Matrix](../practice/array/48-spiral-matrix.md)
- [49. Set Matrix Zeroes](../practice/array/49-set-matrix-zeroes.md)
- [50. Rotate Image](../practice/array/50-rotate-image.md)
