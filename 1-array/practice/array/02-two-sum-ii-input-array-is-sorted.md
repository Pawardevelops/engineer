# 02. Two Sum II - Input Array Is Sorted

## Links

- LeetCode: [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- Pattern: [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find two numbers in a sorted array whose sum equals the target and return their 1-based positions.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Sorted order lets one comparison remove many pairs. A small sum means every pair using the current left with a smaller right is also too small.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Check every pair until the target is found. It works but ignores the sorted order and takes O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Place left at the first element and right at the last.
2. Compute the current sum.
3. Return indexes if it matches target.
4. Move left rightward if the sum is too small.
5. Move right leftward if the sum is too large.

## Dry Run

Use a small input for `Two Sum II - Input Array Is Sorted` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers) - 1

        while left < right:
            current = numbers[left] + numbers[right]

            if current == target:
                return [left + 1, right + 1]
            if current < target:
                left += 1
            else:
                right -= 1

        return []
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Returning 0-based indexes.
- Using hashing and missing the sorted-array lesson.
- Moving the wrong side after comparing the sum.

## What You Should Learn

Sorted order converts pair search into controlled boundary movement.
