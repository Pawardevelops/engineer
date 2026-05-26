# Monotonic Stack

## Core Idea

Maintain a stack whose values or indexes stay increasing or decreasing. Pop elements when the current value proves their answer.

## Why This Pattern Exists

Next greater or next smaller questions look backward many times. A monotonic stack keeps only unresolved candidates that still have a chance.

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

- The question asks for next greater, next smaller, previous greater, or a waiting time.
- Each element needs the nearest future or previous element satisfying a comparison.
- A new element can resolve many older elements at once.
- A circular array can be handled by scanning twice.

## When Not To Use It

- You need arbitrary range maximum queries many times, where a segment tree may fit better.
- The relationship is not based on nearest greater or smaller comparisons.
- The problem requires sorted global order, not local next relationships.

## Common Shapes

### Next greater to right
Keep decreasing stack of unresolved indexes.

### Next smaller to right
Keep increasing stack of unresolved indexes.

### Circular next greater
Scan 2n positions and use modulo indexes.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def next_greater(nums: List[int]) -> List[int]:
    answer = [-1] * len(nums)
    stack = []

    for i, value in enumerate(nums):
        while stack and nums[stack[-1]] < value:
            j = stack.pop()
            answer[j] = value
        stack.append(i)

    return answer
```

## Worked Mini Examples

### Daily temperatures
A warmer day resolves all colder days on top of the stack.

### Next greater element II
Scanning twice lets earlier elements see values after wraparound.

### Stock span style
Popping smaller previous values gives a compact history.

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Storing values when indexes are needed to compute distance.
- Using `<` versus `<=` incorrectly when duplicates exist.
- For circular arrays, pushing indexes during both passes and creating duplicates.

## Questions Using This Pattern

- [45. Daily Temperatures](../practice/array/45-daily-temperatures.md)
- [46. Asteroid Collision](../practice/array/46-asteroid-collision.md)
- [47. Next Greater Element II](../practice/array/47-next-greater-element-ii.md)
