# 21. Kth Largest Element in an Array

## Links

- LeetCode: [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- Pattern: [Heap And Selection](../../patterns/heap-and-selection.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return the kth largest value in an unsorted array.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The kth largest is the element at index n - k if the array were sorted ascending. Quickselect partitions until that index is fixed.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Sort the full array and index into it. That is simple O(n log n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Convert kth largest to target sorted index n - k.
2. Partition around a pivot.
3. If pivot lands at target, return it.
4. If pivot is too far left, search right.
5. If pivot is too far right, search left.

## Dry Run

Use a small input for `Kth Largest Element in an Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findKthLargest(self, nums: List[int], k: int) -> int:
        target = len(nums) - k
        left, right = 0, len(nums) - 1

        def partition(lo: int, hi: int) -> int:
            pivot = nums[hi]
            store = lo
            for i in range(lo, hi):
                if nums[i] <= pivot:
                    nums[store], nums[i] = nums[i], nums[store]
                    store += 1
            nums[store], nums[hi] = nums[hi], nums[store]
            return store

        while True:
            pivot_index = partition(left, right)
            if pivot_index == target:
                return nums[pivot_index]
            if pivot_index < target:
                left = pivot_index + 1
            else:
                right = pivot_index - 1
```

## Complexity Analysis

Average time O(n), worst-case O(n^2), space O(1).

## Common Mistakes

- Using k directly instead of n - k for ascending rank.
- Partitioning but searching both sides.
- Forgetting quickselect mutates the array.

## What You Should Learn

Selection asks for one rank, so only one partition side remains relevant.
