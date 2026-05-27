# Boyer-Moore Voting

## Core Idea

Cancel different values against each other to identify possible majority candidates using constant space.

## Visual Mental Model

Think of different values canceling each other out.

```text
nums = [2, 2, 1, 1, 1, 2, 2]

candidate = 2, count = 1
see 2 -> count = 2
see 1 -> count = 1
see 1 -> count = 0
candidate can change
```

If a value appears more than half the time, it survives all cancellations.

## Why This Pattern Exists

If a value appears more than n/2 or n/3 times, it cannot be completely canceled by all other values.

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

- The question asks for elements appearing more than n/2 or n/3 times.
- O(1) extra space is desired.
- You only need candidates first, then verify them.
- The threshold limits how many answers can exist.

## When Not To Use It

- You need exact counts for every value.
- The threshold allows many possible answers.
- The problem does not involve a strict frequency majority.

## Common Shapes

### One candidate
For more than n/2, keep one candidate and one counter.

### Two candidates
For more than n/3, keep two candidates and two counters.

### Verification pass
Count candidates again because the first pass only finds possibilities.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def majority_over_half(nums: List[int]) -> int:
    candidate = None
    count = 0

    for value in nums:
        if count == 0:
            candidate = value
        count += 1 if value == candidate else -1

    return candidate
```

## Worked Mini Examples

### Majority element
A true majority survives pair cancellation.

### Majority element II
At most two numbers can appear more than n/3 times.

### Streaming candidate
The algorithm keeps only candidates and counters while scanning once.

## Three Warm-Up Questions

| No. | Question | Why It Helps |
|---|---|---|
| 1 | [Majority Element](https://leetcode.com/problems/majority-element/) | One-candidate Boyer-Moore. |
| 2 | [Majority Element II](https://leetcode.com/problems/majority-element-ii/) | Two-candidate Boyer-Moore. |
| 3 | [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) | Compare hashmap frequency thinking before constant-space voting. |

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

- Skipping the verification pass when the threshold is not guaranteed.
- Allowing both candidates to become the same value.
- Thinking the counter is the real frequency.

## Questions Using This Pattern

- [22. Majority Element II](../practice/array/22-majority-element-ii.md)
