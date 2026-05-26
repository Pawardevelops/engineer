# Binary Search On Answer

## Core Idea

Binary search the value of the answer, not an array index. A helper function checks whether a candidate answer is feasible.

## Why This Pattern Exists

Some problems ask for the minimum speed, capacity, distance, or value that satisfies a condition. If feasibility changes monotonically, binary search can find the boundary.

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

- The answer is a number inside a known range.
- You can test a candidate answer in O(n) or similar time.
- If candidate x works, every larger candidate also works, or the reverse.
- The prompt asks to minimize the maximum, maximize the minimum, or find the smallest valid rate.

## When Not To Use It

- Feasibility is not monotonic.
- You cannot define clear low and high bounds.
- A direct formula gives the answer.

## Common Shapes

### Minimize feasible value
Move right down when mid works.

### Maximize feasible value
Move left up when mid works.

### Counting feasibility
Count how many items can be placed, processed, or kept under candidate x.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def minimum_feasible(low: int, high: int, can_do) -> int:
    while low < high:
        mid = (low + high) // 2
        if can_do(mid):
            high = mid
        else:
            low = mid + 1

    return low
```

## Worked Mini Examples

### Koko eating bananas
If speed s works, any faster speed also works.

### Ship packages
If capacity c works, any larger capacity also works.

### Magnetic force
If distance d can be achieved, smaller distances can also be achieved.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Choosing bounds that exclude the real answer.
- Writing a feasibility function with side effects that change between checks.
- Using the minimize template for a maximize problem without changing the movement.

## Questions Using This Pattern

- [24. Find the Duplicate Number](../practice/array/24-find-the-duplicate-number.md)
- [32. Koko Eating Bananas](../practice/array/32-koko-eating-bananas.md)
- [33. Capacity To Ship Packages Within D Days](../practice/array/33-capacity-to-ship-packages-within-d-days.md)
- [34. Magnetic Force Between Two Balls](../practice/array/34-magnetic-force-between-two-balls.md)
