# 07. Remove Duplicates From Sorted Array II

## Links

- LeetCode: [Remove Duplicates From Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)
- Pattern: [In-Place Array Techniques](../../patterns/in-place-array-techniques.md), [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Modify a sorted array so each value appears at most twice and return the new length.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Sorted duplicates are adjacent. A write pointer can build the valid prefix while a read loop scans every value once.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Build a new list with allowed values and copy it back. That is easy but uses extra memory.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Keep write as the length of the valid prefix.
2. For each value, allow it if fewer than two values have been written.
3. Otherwise compare with nums[write - 2].
4. If different, writing this value keeps at most two copies.
5. Return write.

## Dry Run

Use a small input for `Remove Duplicates From Sorted Array II` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def removeDuplicates(self, nums: List[int]) -> int:
        write = 0

        for value in nums:
            if write < 2 or nums[write - 2] != value:
                nums[write] = value
                write += 1

        return write
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Comparing with nums[write - 1] instead of nums[write - 2].
- Deleting elements from the middle repeatedly.
- Returning len(nums) instead of the compacted length.

## What You Should Learn

The valid prefix idea is more important than physically removing elements.
