# 23. Find All Duplicates in an Array

## Links

- LeetCode: [Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/)
- Pattern: [In-Place Array Techniques](../../patterns/in-place-array-techniques.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find all values that appear twice in an array where values are between 1 and n.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Value x maps to index x - 1. Negating nums[x - 1] marks that x has been seen; seeing it already negative means duplicate.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Use a set or hashmap to count duplicates. That uses extra memory.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. For each value, use abs(value) because previous marks may be negative.
2. Map value to index value - 1.
3. If nums[index] is already negative, value is a duplicate.
4. Otherwise negate nums[index].
5. Return collected duplicates.

## Dry Run

Use a small input for `Find All Duplicates in an Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findDuplicates(self, nums: List[int]) -> List[int]:
        duplicates = []

        for value in nums:
            index = abs(value) - 1
            if nums[index] < 0:
                duplicates.append(abs(value))
            else:
                nums[index] = -nums[index]

        return duplicates
```

## Complexity Analysis

Time O(n), space O(1) extra besides output.

## Common Mistakes

- Using value directly instead of value - 1.
- Forgetting abs(value).
- Applying this trick when values are not constrained to 1..n.

## What You Should Learn

When values fit the index range, the array can act like its own hashmap.
