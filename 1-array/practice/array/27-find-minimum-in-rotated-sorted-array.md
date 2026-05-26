# 27. Find Minimum in Rotated Sorted Array

## Links

- LeetCode: [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- Pattern: [Binary Search On Arrays](../../patterns/binary-search.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return the minimum value in a rotated sorted array with unique values.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If nums[mid] is greater than nums[right], the minimum must be to the right of mid. Otherwise mid could be the minimum, so keep the left side including mid.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Scan the array and track the minimum in O(n).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Set left and right at array ends.
2. Compute mid.
3. If nums[mid] > nums[right], move left to mid + 1.
4. Otherwise move right to mid.
5. When left equals right, it points to the minimum.

## Dry Run

Use a small input for `Find Minimum in Rotated Sorted Array` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1

        while left < right:
            mid = (left + right) // 2

            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                right = mid

        return nums[left]
```

## Complexity Analysis

Time O(log n), space O(1).

## Common Mistakes

- Using right = mid - 1 and accidentally discarding mid.
- Comparing against nums[left] without handling cases carefully.
- Forgetting the unrotated array still works.

## What You Should Learn

Boundary binary search often keeps mid when mid can still be the answer.
