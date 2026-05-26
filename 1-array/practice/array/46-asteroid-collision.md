# 46. Asteroid Collision

## Links

- LeetCode: [Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)
- Pattern: [Monotonic Stack](../../patterns/monotonic-stack.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Asteroids move left or right based on sign. When a right-moving asteroid meets a left-moving asteroid, the smaller one explodes.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

Only a previous positive asteroid can collide with a current negative asteroid. A stack stores surviving asteroids to the left.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Brute Force Thinking

Simulate collisions by repeatedly scanning adjacent pairs until no changes occur. That can be slow.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. For each asteroid, assume it is alive.
2. While it moves left and stack top moves right, resolve collision.
3. Pop smaller right-moving asteroids.
4. Destroy current if stack top is larger.
5. Pop both if equal; otherwise append surviving current.

## Dry Run

Use a small input for `Asteroid Collision` and track every state variable from the algorithm. The goal is to explain why each update is legal, not just what the code does.

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
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []

        for asteroid in asteroids:
            alive = True

            while alive and asteroid < 0 and stack and stack[-1] > 0:
                if stack[-1] < -asteroid:
                    stack.pop()
                    continue
                if stack[-1] == -asteroid:
                    stack.pop()
                alive = False

            if alive:
                stack.append(asteroid)

        return stack
```

## Complexity Analysis

Time O(n), space O(n).

## Common Mistakes

- Colliding asteroids moving away from each other.
- Stopping after popping one smaller asteroid when more collisions may follow.
- Appending a destroyed current asteroid.

## What You Should Learn

Stack simulations work when only the nearest unresolved left neighbor can interact with the current item.
