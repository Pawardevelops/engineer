# Greedy Array Decisions

## Core Idea

Make the locally best decision that can be proven not to hurt the future answer.

## Visual Mental Model

Greedy is about keeping the strongest useful state so far.

Jump Game:

```text
nums = [2, 3, 1, 1, 4]

index 0 reaches up to 2
index 1 reaches up to 4

farthest = 4, so the end is reachable.
```

Gas Station:

```text
If tank becomes negative at station i,
then no station in the failed segment can be the start.
Restart at i + 1.
```

## Why This Pattern Exists

Some array problems are really about maintaining the strongest possible state while scanning once.

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

- A local state summarizes everything useful so far.
- The problem asks for reachability, minimum jumps, start position, or keeping non-overlapping items.
- You can prove that a worse current state is never useful later.
- Sorting by a key creates a safe local choice.

## When Not To Use It

- A local choice can block a better global arrangement and no exchange argument exists.
- The problem asks to count all ways.
- The state space has multiple dimensions that require dynamic programming.

## Common Shapes

### Farthest reach
Keep the farthest index reachable so far.

### Layered jumps
Treat all positions inside current reach as one jump layer.

### Reset start
When current balance becomes impossible, the next index becomes the only possible start.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def can_reach_end(nums: List[int]) -> bool:
    farthest = 0

    for i, jump in enumerate(nums):
        if i > farthest:
            return False
        farthest = max(farthest, i + jump)

    return True
```

## Worked Mini Examples

### Jump game
If every index up to i is reachable, only the farthest reach matters.

### Jump game II
When you finish the current layer, you must spend one jump.

### Gas station
A negative tank means no station in the failed segment can be the answer.

## Three Warm-Up Questions

| No. | Question | Why It Helps |
|---|---|---|
| 1 | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | Keep the best state seen so far. |
| 2 | [Can Place Flowers](https://leetcode.com/problems/can-place-flowers/) | Local placement decisions. |
| 3 | [Lemonade Change](https://leetcode.com/problems/lemonade-change/) | Greedy resource management. |

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

- Using greedy without a reason why local discard is safe.
- Updating the answer after the state has already become impossible.
- Confusing reachability with minimum number of moves.

## Questions Using This Pattern

- [37. Non-overlapping Intervals](../practice/array/37-non-overlapping-intervals.md)
- [38. Minimum Number of Arrows to Burst Balloons](../practice/array/38-minimum-number-of-arrows-to-burst-balloons.md)
- [39. Gas Station](../practice/array/39-gas-station.md)
- [40. Jump Game](../practice/array/40-jump-game.md)
- [41. Jump Game II](../practice/array/41-jump-game-ii.md)
