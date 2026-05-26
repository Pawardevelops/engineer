# 06. Sort Colors

## Links

- LeetCode: [Sort Colors](https://leetcode.com/problems/sort-colors/)
- Pattern: [In-Place Array Techniques](../../patterns/in-place-array-techniques.md), [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Rearrange an array containing only 0, 1, and 2 so equal values are grouped in sorted order.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Because there are only three values, the array can be divided into 0-region, unknown-region, and 2-region without extra memory.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Count each value and overwrite the array. That is linear but uses the counting idea instead of the intended one-pass partition.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Keep low for next 0, mid for current unknown, and high for next 2.
2. If nums[mid] is 0, swap with low and advance both.
3. If nums[mid] is 1, advance mid.
4. If nums[mid] is 2, swap with high and decrease high.
5. Do not advance mid after swapping with high because the incoming value is still unknown.

## Dry Run

Use a small input for `Sort Colors` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def sortColors(self, nums: List[int]) -> None:
        low, mid, high = 0, 0, len(nums) - 1

        while mid <= high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                mid += 1
            else:
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Advancing mid after swapping with high.
- Using sorting and missing the partition invariant.
- Letting the loop stop at mid < high instead of mid <= high.

## What You Should Learn

In-place partitioning works when every pointer owns a clear region invariant.
