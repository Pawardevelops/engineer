# 39. Gas Station

## Links

- LeetCode: [Gas Station](https://leetcode.com/problems/gas-station/)
- Pattern: [Greedy Array Decisions](../../patterns/greedy-arrays.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Find a starting gas station index from which you can complete the circular route, or return -1.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

If total gas is less than total cost, no answer exists. If the tank becomes negative at i, no station in the current segment can be a valid start.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Try starting from every station and simulate the full route. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Check total gas versus total cost.
2. Scan stations while tracking current tank.
3. If tank becomes negative, set start to i + 1 and reset tank.
4. Continue scanning.
5. Return start.

## Dry Run

Use a small input for `Gas Station` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas) < sum(cost):
            return -1

        start = 0
        tank = 0

        for i in range(len(gas)):
            tank += gas[i] - cost[i]
            if tank < 0:
                start = i + 1
                tank = 0

        return start
```

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Trying every start despite the discard proof.
- Forgetting the total feasibility check.
- Resetting start without resetting tank.

## What You Should Learn

A negative prefix proves every start inside that failed prefix is impossible.
