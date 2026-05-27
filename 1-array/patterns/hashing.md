# Hashing With Arrays

## Core Idea

Use a set or dictionary to remember values, counts, first positions, or relationships that would otherwise require repeated scans.

## Visual Mental Model

Hashing adds memory to a left-to-right scan.

```text
nums = [4, 2, 7, 2, 9]

scan value: 4     seen = {4}
scan value: 2     seen = {4, 2}
scan value: 7     seen = {4, 2, 7}
scan value: 2     already seen -> duplicate found
```

For frequency questions:

```text
nums = [1, 1, 1, 2, 2, 3]

counts:
1 -> 3
2 -> 2
3 -> 1
```

The array gives order. The hashmap gives memory.

## Why This Pattern Exists

Arrays are ordered, but many problems need fast lookup by value. Hashing adds O(1)-average lookup so each element can usually be processed once.

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

- You repeatedly ask whether a value has appeared before.
- You need frequency counts.
- You need to remember the earliest index for a state.
- The array order matters, but sorting would destroy the original relationship.

## When Not To Use It

- The array is already sorted and a two-pointer solution is simpler.
- You need ordered queries such as next greater or lower bound.
- The problem requires strict O(1) extra space and the array can be modified in-place.

## Common Shapes

### Set membership
Remember values and test complements or sequence starts.

### Frequency map
Count occurrences and make decisions from frequencies.

### State to index
Remember the first time a prefix state appeared to maximize length.

## Recognition Questions

Ask these before choosing the pattern:

- Is the array sorted, or can I sort it without breaking the answer?
- Is the answer about a contiguous subarray, a pair, a boundary, or a rank?
- Can one local comparison safely remove many candidates?
- What invariant must stay true after every pointer move, stack update, or scan step?

## Python Template

```python
from typing import List


def longest_consecutive(nums: List[int]) -> int:
    values = set(nums)
    best = 0

    for value in values:
        if value - 1 in values:
            continue

        length = 1
        while value + length in values:
            length += 1

        best = max(best, length)

    return best
```

## Worked Mini Examples

### Longest consecutive sequence
A set lets you start only at sequence beginnings.

### Top K frequent
A frequency map converts raw values into counts.

### Prefix balance
A map from balance to first index reveals the longest matching span.

## Three Easy Warm-Up Questions

| No. | Question | Why It Helps |
|---|---|---|
| 1 | [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) | Basic set membership. |
| 2 | [Two Sum](https://leetcode.com/problems/two-sum/) | Store complements or previous values. |
| 3 | [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/) | Set operations on arrays. |
 
## Study Links

- [NeetCode Practice](https://neetcode.io/practice)
- [LeetCode 75](https://leetcode.com/studyplan/leetcode-75/)
- [VisuAlgo](https://visualgo.net/)

## How To Dry Run This Pattern

1. Write the current state variables before the loop.
2. Process one element or one pointer move at a time.
3. After each move, ask whether the invariant is still true.
4. Update the answer only at the correct time: after restoring validity for max-window problems, or before shrinking for min-window problems.
5. Test edge cases: empty-like boundaries, one element, duplicates, all same values, and no-answer cases.

## Common Mistakes

- Scanning forward from every value instead of only sequence starts.
- Assuming hash maps are sorted.
- Overwriting the first index when the earliest index gives the longest answer.

## Questions Using This Pattern

- [11. Subarray Sum Equals K](../practice/array/11-subarray-sum-equals-k.md)
- [12. Continuous Subarray Sum](../practice/array/12-continuous-subarray-sum.md)
- [13. Contiguous Array](../practice/array/13-contiguous-array.md)
- [16. Fruit Into Baskets](../practice/array/16-fruit-into-baskets.md)
- [19. Longest Consecutive Sequence](../practice/array/19-longest-consecutive-sequence.md)
- [20. Top K Frequent Elements](../practice/array/20-top-k-frequent-elements.md)
