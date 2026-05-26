# 30. Single Element in a Sorted Array

## Links

- LeetCode: [Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Every value appears exactly twice except one value that appears once. Find the single value.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Before the single element, pairs start at even indexes. After it, pair alignment flips. Binary search detects where the flip begins.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

XOR all values or scan pairs. XOR is O(n), but the sorted array allows O(log n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Use mid as the start of a pair by making it even.
2. If nums[mid] == nums[mid + 1], the single value is after that pair.
3. Otherwise it is at mid or before.
4. Continue until left == right.
5. Return nums[left].

## Dry Run

Use a small input for `Single Element in a Sorted Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def singleNonDuplicate(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1

        while left < right:
            mid = (left + right) // 2
            if mid % 2 == 1:
                mid -= 1

            if nums[mid] == nums[mid + 1]:
                left = mid + 2
            else:
                right = mid

        return nums[left]
```

## Complexity Analysis

Time O(log n), space O(1).

## Common Mistakes

- Letting mid be odd and comparing the wrong pair.
- Using XOR and missing the binary-search practice.
- Setting right = mid - 1 when mid can be the answer.

## What You Should Learn

Index parity can be a monotonic signal in sorted arrays.
