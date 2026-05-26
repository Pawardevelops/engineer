# Prefix Sum

## Core Idea

Store or track cumulative information so the sum of a range can be computed from two prefix values.

## Why This Pattern Exists

Subarray sum problems often ask the same question many times: what is the sum from i to j? Prefix sums turn that repeated work into arithmetic.

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

- The problem asks about subarray sums, counts, balances, or remainders.
- Negative numbers are allowed, making sliding window unreliable.
- You need to know whether a previous cumulative state has appeared.
- The condition can be written as current_prefix - previous_prefix = target.

## When Not To Use It

- The problem only needs one running sum over a positive window.
- The operation is not reversible, such as maximum or mode over arbitrary ranges.
- The answer depends on element order after sorting.

## Common Shapes

### Range sum
Build an array where prefix[i] stores the sum before index i.

### Prefix plus hashmap
Store how often each prefix value has appeared to count subarrays ending at the current index.

### Prefix modulo
Store first index of each remainder to reason about divisibility.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from collections import defaultdict
from typing import List


def count_subarrays_with_sum(nums: List[int], target: int) -> int:
    seen = defaultdict(int)
    seen[0] = 1
    prefix = 0
    count = 0

    for value in nums:
        prefix += value
        count += seen[prefix - target]
        seen[prefix] += 1

    return count
```

## Worked Mini Examples

### Subarray sum equals k
If current prefix is p, then any earlier prefix p-k creates a valid subarray.

### Continuous subarray sum
Two prefixes with the same remainder differ by a multiple of k.

### Contiguous binary array
Treat 0 as -1 and 1 as +1; equal balance means equal zeros and ones.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Forgetting to seed prefix value 0 before scanning.
- Using a set when counts are required.
- Confusing prefix indexes with array indexes in length problems.

## Questions Using This Pattern

- [10. Product of Array Except Self](../practice/array/10-product-of-array-except-self.md)
- [11. Subarray Sum Equals K](../practice/array/11-subarray-sum-equals-k.md)
- [12. Continuous Subarray Sum](../practice/array/12-continuous-subarray-sum.md)
- [13. Contiguous Array](../practice/array/13-contiguous-array.md)
- [18. Minimum Operations to Reduce X to Zero](../practice/array/18-minimum-operations-to-reduce-x-to-zero.md)
