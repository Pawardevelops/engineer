# In-Place Array Techniques

## Core Idea

Modify the input array directly using swaps, reversals, write pointers, signs, or reserved marker positions.

## Visual Mental Model

In-place means the array itself becomes the workspace.

Write pointer:

```text
nums = [0, 1, 0, 3, 12]

read scans all values
write marks where the next non-zero should go

[0, 1, 0, 3, 12]
 W  R
```

Index marking:

```text
value x marks index x - 1

value 3 -> mark index 2
value 1 -> mark index 0
```

Reversal:

```text
[1, 2, 3, 4, 5]
 reverse all -> [5, 4, 3, 2, 1]
```

## Why This Pattern Exists

Interview array questions often add an O(1) extra-space requirement. In-place techniques use the array itself as working memory.

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

- The problem explicitly asks for in-place modification.
- Values are constrained enough to use indexes as markers.
- The array is sorted and can be compacted with a write pointer.
- A transformation can be built from swaps or reversals.

## When Not To Use It

- The input must remain unchanged.
- Values are outside indexable range and cannot be safely marked.
- The in-place version becomes much harder while extra memory is allowed.

## Common Shapes

### Write pointer
Read every element and overwrite the valid prefix.

### Index marking
Use sign changes or swaps to mark that a value has been seen.

### Reverse sections
Rotate or permute by reversing meaningful ranges.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def reverse_range(nums: List[int], left: int, right: int) -> None:
    while left < right:
        nums[left], nums[right] = nums[right], nums[left]
        left += 1
        right -= 1
```

## Worked Mini Examples

### Sort colors
Three regions represent 0s, 1s, and 2s.

### Find duplicates
Negating nums[abs(x)-1] marks that x has appeared.

### Rotate array
Reverse all, then reverse each rotated part.

## Three Easy Warm-Up Questions

| No. | Question | Why It Helps |
|---|---|---|
| 1 | [Move Zeroes](https://leetcode.com/problems/move-zeroes/) | Write pointer compaction. |
| 2 | [Remove Element](https://leetcode.com/problems/remove-element/) | Overwrite unwanted values. |
| 3 | [Reverse String](https://leetcode.com/problems/reverse-string/) | Basic in-place swapping. |

## Study Links

- [NeetCode Practice](https://neetcode.io/practice)
- [VisuAlgo](https://visualgo.net/)

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Forgetting that marked values may be negative and need abs().
- Incrementing the scan pointer after swapping from the unknown region.
- Using O(n) extra memory when the goal is specifically O(1).

## Questions Using This Pattern

- [06. Sort Colors](../practice/array/06-sort-colors.md)
- [07. Remove Duplicates From Sorted Array II](../practice/array/07-remove-duplicates-from-sorted-array-ii.md)
- [08. Next Permutation](../practice/array/08-next-permutation.md)
- [09. Rotate Array](../practice/array/09-rotate-array.md)
- [23. Find All Duplicates in an Array](../practice/array/23-find-all-duplicates-in-an-array.md)
- [49. Set Matrix Zeroes](../practice/array/49-set-matrix-zeroes.md)
- [50. Rotate Image](../practice/array/50-rotate-image.md)
