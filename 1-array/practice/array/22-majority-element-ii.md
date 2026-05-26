# 22. Majority Element II

## Links

- LeetCode: [Majority Element II](https://leetcode.com/problems/majority-element-ii/)
- Pattern: [Boyer-Moore Voting](../../patterns/boyer-moore-voting.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Return all values that appear more than floor(n / 3) times.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

There can be at most two such values. Boyer-Moore keeps two candidates and cancels groups of three different values.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Count every value with a hashmap. That is O(n) time but O(n) space.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Find up to two candidates with counters.
2. When a value matches a candidate, increment its counter.
3. When a counter is zero, replace that candidate.
4. Otherwise decrement both counters.
5. Verify the final candidates with real counts.

## Dry Run

Use a small input for `Majority Element II` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def majorityElement(self, nums: List[int]) -> List[int]:
        cand1 = cand2 = None
        count1 = count2 = 0

        for value in nums:
            if value == cand1:
                count1 += 1
            elif value == cand2:
                count2 += 1
            elif count1 == 0:
                cand1 = value
                count1 = 1
            elif count2 == 0:
                cand2 = value
                count2 = 1
            else:
                count1 -= 1
                count2 -= 1

        result = []
        for candidate in (cand1, cand2):
            if candidate is not None and nums.count(candidate) > len(nums) // 3:
                if candidate not in result:
                    result.append(candidate)

        return result
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Skipping verification.
- Letting cand1 and cand2 represent the same value.
- Thinking the final counters are exact frequencies.

## What You Should Learn

Majority thresholds limit how many candidates can survive cancellation.
