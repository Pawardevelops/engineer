# 11. Subarray Sum Equals K

## Links

- LeetCode: [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
- Pattern: [Prefix Sum](../../patterns/prefix-sum.md), [Hashing With Arrays](../../patterns/hashing.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Count how many contiguous subarrays have sum exactly k.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If current prefix is p, then any previous prefix p - k forms a subarray ending here with sum k. A hashmap stores how often each prefix occurred.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Visual Explanation

Example:

```text
nums = [1, 2, 3]
k = 3
```

Prefix sums:

```text
before array: prefix = 0
after 1:      prefix = 1
after 2:      prefix = 3
after 3:      prefix = 6
```

At each index, we ask:

```text
current_prefix - old_prefix = k
```

Rearrange:

```text
old_prefix = current_prefix - k
```

So if:

```text
current_prefix = 3
k = 3
old_prefix needed = 0
```

We have seen prefix `0` before the array started, so subarray `[1, 2]` is valid.

Later:

```text
current_prefix = 6
k = 3
old_prefix needed = 3
```

We have seen prefix `3`, so subarray `[3]` is valid.

That gives two subarrays.

## Brute Force Thinking

Try every start and end, computing sums. Even with incremental sums this is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Start with seen[0] = 1 to count subarrays beginning at index 0.
2. Scan values and update prefix.
3. Add seen[prefix - k] to the answer.
4. Record the current prefix.
5. Continue until the end.

## Dry Run

Input:

```text
nums = [1, 2, 3]
k = 3
```

Start:

```text
seen = {0: 1}
prefix = 0
count = 0
```

| Step | value | prefix | needed prefix `prefix - k` | seen needed count | count | seen after |
|---|---:|---:|---:|---:|---:|---|
| 1 | 1 | 1 | -2 | 0 | 0 | {0: 1, 1: 1} |
| 2 | 2 | 3 | 0 | 1 | 1 | {0: 1, 1: 1, 3: 1} |
| 3 | 3 | 6 | 3 | 1 | 2 | {0: 1, 1: 1, 3: 1, 6: 1} |

Final answer:

```text
2
```

## Python Solution

```python
from collections import defaultdict
from typing import List


class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        seen = defaultdict(int)
        seen[0] = 1
        prefix = 0
        count = 0

        for value in nums:
            prefix += value
            count += seen[prefix - k]
            seen[prefix] += 1

        return count
```

## Line-By-Line Explanation

```text
seen[0] = 1
```

This handles subarrays that start at index `0`.

```text
prefix += value
```

Now `prefix` is the sum from the beginning up to the current index.

```text
count += seen[prefix - k]
```

Every previous prefix equal to `prefix - k` creates a subarray ending here with sum `k`.

```text
seen[prefix] += 1
```

Record the current prefix so future indexes can use it.

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Using a set instead of counts.
- Forgetting seen[0] = 1.
- Trying sliding window with negative numbers.

## What You Should Learn

Counting subarrays usually needs frequency of prefix states, not just whether a state exists.
