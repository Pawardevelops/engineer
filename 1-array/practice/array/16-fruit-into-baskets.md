# 16. Fruit Into Baskets

## Links

- LeetCode: [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
- Pattern: [Sliding Window](../../patterns/sliding-window.md), [Hashing With Arrays](../../patterns/hashing.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find the longest contiguous segment containing at most two distinct fruit types.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A window is valid while it has at most two distinct values. A hashmap tracks counts so the left side can shrink correctly.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Start at every index and extend until a third type appears. That can be O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Expand right and increment that fruit count.
2. While the map has more than two keys, decrement fruits[left].
3. Remove a key when its count becomes zero.
4. Update best after the window is valid.
5. Return best.

## Dry Run

Use a small input for `Fruit Into Baskets` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

Suggested dry-run table:

| Step | Current Input Position | Important State | Decision | Why |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |

## Python Solution

```python
from collections import defaultdict
from typing import List


class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        counts = defaultdict(int)
        left = 0
        best = 0

        for right, fruit in enumerate(fruits):
            counts[fruit] += 1

            while len(counts) > 2:
                counts[fruits[left]] -= 1
                if counts[fruits[left]] == 0:
                    del counts[fruits[left]]
                left += 1

            best = max(best, right - left + 1)

        return best
```

## Complexity Analysis

Time O(n), space O(1) because at most three fruit types are stored during shrinking.

## Common Mistakes

- Removing a fruit type before its count reaches zero.
- Updating best while the window still has three types.
- Thinking this is about choosing any fruits rather than a contiguous segment.

## What You Should Learn

Frequency maps are often the state that makes variable sliding windows work.
