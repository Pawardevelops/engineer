# 45. Daily Temperatures

## Links

- LeetCode: [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
- Pattern: [Monotonic Stack](../../patterns/monotonic-stack.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

For each day, return how many days you wait until a warmer temperature appears.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

A warmer current day resolves all earlier colder days on top of the stack. The stack keeps unresolved days in decreasing temperature order.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

For each day, scan forward until a warmer day is found. That is O(n^2).

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Create answer array of zeros.
2. Keep a stack of unresolved indexes.
3. For each temperature, pop colder indexes.
4. For each popped index, distance is current index minus popped index.
5. Push the current index.

## Dry Run

Use a small input for `Daily Temperatures` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0] * len(temperatures)
        stack = []

        for i, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                prev = stack.pop()
                answer[prev] = i - prev
            stack.append(i)

        return answer
```

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Storing temperatures instead of indexes and losing distance.
- Popping on <= instead of <.
- Scanning forward again for each index.

## What You Should Learn

Monotonic stacks solve many next-greater questions in one pass because each index is pushed and popped once.
