# Kadane And Subarray Optimization

## Core Idea

Track the best subarray ending at the current index and the best answer seen globally.

## Visual Mental Model

At every index, Kadane asks:

```text
Should I extend the previous subarray,
or should I start fresh here?
```

Example:

```text
nums = [-2, 1, -3, 4, -1, 2, 1]

At value 4:
previous current sum is bad, so start fresh at 4.

At value -1:
4 + -1 = 3 is still useful, so continue.

At value 2:
3 + 2 = 5 is better, continue.
```

## Why This Pattern Exists

For contiguous maximum problems, a bad prefix should be dropped because it can only make any future subarray worse.

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

- The problem asks for maximum or minimum sum/product over a contiguous subarray.
- The best subarray ending here can be derived from the previous best ending one step before.
- A negative or harmful prefix should be reset.
- The array can contain negative values.

## When Not To Use It

- The selected elements do not need to be contiguous.
- The problem needs the actual list of all optimal subarrays.
- The transition depends on many previous positions instead of only local carried state.

## Common Shapes

### Maximum sum
current = max(value, current + value).

### Maximum product
Track both max and min ending here because a negative value swaps them.

### Circular maximum
Compare normal max subarray with total sum minus minimum subarray.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def max_subarray_sum(nums: List[int]) -> int:
    current = nums[0]
    best = nums[0]

    for value in nums[1:]:
        current = max(value, current + value)
        best = max(best, current)

    return best
```

## Worked Mini Examples

### Maximum subarray
A negative running sum is discarded before it hurts future sums.

### Maximum product subarray
The smallest negative product may become the largest after multiplying by a negative.

### Circular subarray
The wrapped answer is everything except the weakest middle segment.

## Three Warm-Up Questions

| No. | Question | Why It Helps |
|---|---|---|
| 1 | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | Same idea of keeping the best local state. |
| 2 | [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) | The core Kadane problem. |
| 3 | [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) | Kadane with both min and max state. |

## Study Links

- [NeetCode Practice](https://neetcode.io/practice)
- [LeetCode 75](https://leetcode.com/studyplan/leetcode-75/)

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Initializing the answer to 0 when all numbers may be negative.
- For maximum product, tracking only the maximum and forgetting the minimum.
- For circular arrays, returning 0 for all-negative inputs.

## Questions Using This Pattern

- [42. Maximum Subarray](../practice/array/42-maximum-subarray.md)
- [43. Maximum Product Subarray](../practice/array/43-maximum-product-subarray.md)
- [44. Maximum Sum Circular Subarray](../practice/array/44-maximum-sum-circular-subarray.md)
