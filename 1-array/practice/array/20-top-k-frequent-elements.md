# 20. Top K Frequent Elements

## Links

- LeetCode: [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- Pattern: [Hashing With Arrays](../../patterns/hashing.md), [Heap And Selection](../../patterns/heap-and-selection.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return the k values that appear most often in the array.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A hashmap counts frequencies. Since frequency is between 1 and n, buckets let us collect high-frequency values without sorting all items.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Count frequencies, sort all unique values by count, and take k. That is O(m log m) for m unique values.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Count each value.
2. Create buckets where index represents frequency.
3. Place each value in its frequency bucket.
4. Scan buckets from high to low.
5. Collect values until k results are found.

## Dry Run

Use a small input for `Top K Frequent Elements` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

Suggested dry-run table:

| Step | Current Input Position | Important State | Decision | Why |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |

## Python Solution

```python
from collections import Counter
from typing import List


class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counts = Counter(nums)
        buckets = [[] for _ in range(len(nums) + 1)]

        for value, freq in counts.items():
            buckets[freq].append(value)

        result = []
        for freq in range(len(buckets) - 1, 0, -1):
            for value in buckets[freq]:
                result.append(value)
                if len(result) == k:
                    return result

        return result
```

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Sorting nums itself instead of frequencies.
- Returning frequencies instead of values.
- Assuming bucket output order must be sorted when the problem allows any order.

## What You Should Learn

Frequency problems often split into count first, then select.
