# 24. Find the Duplicate Number

## Links

- LeetCode: [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
- Pattern: [Binary Search On Answer](../../patterns/binary-search-on-answer.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Given n + 1 numbers in range 1..n, find the repeated number without modifying the array.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

For a candidate mid, count how many values are <= mid. If the count is greater than mid, the duplicate must be in the lower half.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Use a set or sort the array. Those violate either space or modification expectations.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Search values from 1 to n.
2. For mid, count numbers <= mid.
3. If count > mid, duplicate lies in left half.
4. Otherwise it lies in right half.
5. Return the boundary value.

## Dry Run

Use a small input for `Find the Duplicate Number` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findDuplicate(self, nums: List[int]) -> int:
        left, right = 1, len(nums) - 1

        while left < right:
            mid = (left + right) // 2
            count = sum(value <= mid for value in nums)

            if count > mid:
                right = mid
            else:
                left = mid + 1

        return left
```

## Complexity Analysis

Time O(n log n), space O(1).

## Common Mistakes

- Binary searching array indexes instead of value range.
- Using count >= mid instead of count > mid.
- Modifying the array when the prompt forbids it.

## What You Should Learn

Binary search on answer works when a count tells which value range is overloaded.
