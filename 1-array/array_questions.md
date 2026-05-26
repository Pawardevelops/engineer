# Array Questions: Top 50 Medium Practice Set

This is the practice index for medium-level array DSA. The goal is not only to solve 50 questions, but to learn the reusable patterns behind them.

Use this flow:

```text
array.md
  -> array_questions.md
  -> patterns/<pattern>.md
  -> practice/array/<question>.md
```

## How To Practice

1. Pick one question from the table.
2. Read the two-line explanation and identify the pattern.
3. Open the linked pattern note and study the core idea.
4. Open the practice file and solve the question in Python.
5. Dry run your code before checking the provided solution.
6. Revisit the same question after a few days and solve it without looking.

## Questions

| No. | Question | Pattern | Two-Line Explanation | Practice |
|---|---|---|---|---|
| 1 | [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | [Two Pointers](patterns/two-pointers.md) | Practice shrinking a search space from both ends. The key lesson is why the shorter boundary is the only boundary worth moving. | [Practice](practice/array/01-container-with-most-water.md) |
| 2 | [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | [Two Pointers](patterns/two-pointers.md) | Shows the cleanest sorted-array two-pointer decision. If the sum is too small move left; if too large move right. | [Practice](practice/array/02-two-sum-ii-input-array-is-sorted.md) |
| 3 | [3Sum](https://leetcode.com/problems/3sum/) | [Sorting-Based Array Patterns](patterns/sorting.md), [Two Pointers](patterns/two-pointers.md) | A classic problem for combining sorting, duplicate handling, and two pointers. It teaches how to reduce a triplet problem to repeated pair problems. | [Practice](practice/array/03-3sum.md) |
| 4 | [3Sum Closest](https://leetcode.com/problems/3sum-closest/) | [Sorting-Based Array Patterns](patterns/sorting.md), [Two Pointers](patterns/two-pointers.md) | Teaches two pointers when you do not need an exact answer. You still use the sum comparison to decide which direction can get closer. | [Practice](practice/array/04-3sum-closest.md) |
| 5 | [4Sum](https://leetcode.com/problems/4sum/) | [Sorting-Based Array Patterns](patterns/sorting.md), [Two Pointers](patterns/two-pointers.md) | Extends 3Sum and forces careful duplicate handling. It is useful for learning how k-sum problems scale. | [Practice](practice/array/05-4sum.md) |
| 6 | [Sort Colors](https://leetcode.com/problems/sort-colors/) | [In-Place Array Techniques](patterns/in-place-array-techniques.md), [Two Pointers](patterns/two-pointers.md) | Introduces the Dutch National Flag partition. It teaches how to maintain multiple in-place regions at once. | [Practice](practice/array/06-sort-colors.md) |
| 7 | [Remove Duplicates From Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) | [In-Place Array Techniques](patterns/in-place-array-techniques.md), [Two Pointers](patterns/two-pointers.md) | Practices write-pointer compaction with a rule. It helps you reason about the valid prefix of an array. | [Practice](practice/array/07-remove-duplicates-from-sorted-array-ii.md) |
| 8 | [Next Permutation](https://leetcode.com/problems/next-permutation/) | [In-Place Array Techniques](patterns/in-place-array-techniques.md) | A strong in-place ordering problem. It teaches how to find the smallest possible increase from the right side. | [Practice](practice/array/08-next-permutation.md) |
| 9 | [Rotate Array](https://leetcode.com/problems/rotate-array/) | [In-Place Array Techniques](patterns/in-place-array-techniques.md) | Practices reversing sections to perform a rotation in-place. It is a simple-looking problem with important index details. | [Practice](practice/array/09-rotate-array.md) |
| 10 | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | [Prefix Sum](patterns/prefix-sum.md) | Teaches prefix/suffix accumulation without division. It shows that prefix ideas are not only for sums. | [Practice](practice/array/10-product-of-array-except-self.md) |
| 11 | [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) | [Prefix Sum](patterns/prefix-sum.md), [Hashing With Arrays](patterns/hashing.md) | One of the most important prefix-sum problems. It teaches why sliding window fails when negative numbers are allowed. | [Practice](practice/array/11-subarray-sum-equals-k.md) |
| 12 | [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/) | [Prefix Sum](patterns/prefix-sum.md), [Hashing With Arrays](patterns/hashing.md) | Introduces prefix remainders. It turns divisibility of a subarray sum into repeated modulo states. | [Practice](practice/array/12-continuous-subarray-sum.md) |
| 13 | [Contiguous Array](https://leetcode.com/problems/contiguous-array/) | [Prefix Sum](patterns/prefix-sum.md), [Hashing With Arrays](patterns/hashing.md) | Shows how to convert a binary-array balance problem into prefix sums. Equal zeros and ones become a repeated balance. | [Practice](practice/array/13-contiguous-array.md) |
| 14 | [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) | [Sliding Window](patterns/sliding-window.md) | A standard variable-size sliding window problem. It teaches expand-until-valid, then shrink-to-optimize. | [Practice](practice/array/14-minimum-size-subarray-sum.md) |
| 15 | [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/) | [Sliding Window](patterns/sliding-window.md) | Builds counting on top of sliding window. Each valid window ending at right contributes multiple subarrays. | [Practice](practice/array/15-subarray-product-less-than-k.md) |
| 16 | [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) | [Sliding Window](patterns/sliding-window.md), [Hashing With Arrays](patterns/hashing.md) | A good variable-window problem with a frequency map. It is the array version of longest substring with at most two distinct values. | [Practice](practice/array/16-fruit-into-baskets.md) |
| 17 | [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) | [Sliding Window](patterns/sliding-window.md) | A clean at-most-k sliding window. It teaches how flipping can be modeled as allowing a limited number of bad elements. | [Practice](practice/array/17-max-consecutive-ones-iii.md) |
| 18 | [Minimum Operations to Reduce X to Zero](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/) | [Sliding Window](patterns/sliding-window.md), [Prefix Sum](patterns/prefix-sum.md) | Teaches problem transformation. Removing from both ends becomes keeping the longest middle subarray. | [Practice](practice/array/18-minimum-operations-to-reduce-x-to-zero.md) |
| 19 | [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | [Hashing With Arrays](patterns/hashing.md) | A core set-based array problem. It teaches how to avoid sorting and still discover sequences. | [Practice](practice/array/19-longest-consecutive-sequence.md) |
| 20 | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | [Hashing With Arrays](patterns/hashing.md), [Heap And Selection](patterns/heap-and-selection.md) | Combines frequency counting with partial selection. It teaches that you often do not need a full sort. | [Practice](practice/array/20-top-k-frequent-elements.md) |
| 21 | [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [Heap And Selection](patterns/heap-and-selection.md) | Introduces quickselect-style rank finding. It teaches why full sorting is unnecessary for one ranked value. | [Practice](practice/array/21-kth-largest-element-in-an-array.md) |
| 22 | [Majority Element II](https://leetcode.com/problems/majority-element-ii/) | [Boyer-Moore Voting](patterns/boyer-moore-voting.md) | A constant-space frequency problem. It teaches why at most two values can appear more than n/3 times. | [Practice](practice/array/22-majority-element-ii.md) |
| 23 | [Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/) | [In-Place Array Techniques](patterns/in-place-array-techniques.md) | Shows how array values can point to indexes. It teaches in-place marking under value-range constraints. | [Practice](practice/array/23-find-all-duplicates-in-an-array.md) |
| 24 | [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) | [Binary Search On Answer](patterns/binary-search-on-answer.md) | Uses binary search on values instead of positions. It teaches how counting can create a monotonic feasibility test. | [Practice](practice/array/24-find-the-duplicate-number.md) |
| 25 | [H-Index](https://leetcode.com/problems/h-index/) | [Sorting-Based Array Patterns](patterns/sorting.md) | A compact sorting problem with a definition-heavy answer. It trains careful interpretation of at least h papers with at least h citations. | [Practice](practice/array/25-h-index.md) |
| 26 | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | [Binary Search On Arrays](patterns/binary-search.md) | A must-know binary search variant. It teaches how to use partial order when the whole array is not normally sorted. | [Practice](practice/array/26-search-in-rotated-sorted-array.md) |
| 27 | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | [Binary Search On Arrays](patterns/binary-search.md) | Focuses binary search on the rotation pivot. It teaches comparing mid with right to locate the unsorted side. | [Practice](practice/array/27-find-minimum-in-rotated-sorted-array.md) |
| 28 | [Find Peak Element](https://leetcode.com/problems/find-peak-element/) | [Binary Search On Arrays](patterns/binary-search.md) | Shows binary search without a globally sorted array. A local slope is enough to choose a side. | [Practice](practice/array/28-find-peak-element.md) |
| 29 | [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | [Binary Search On Arrays](patterns/binary-search.md) | A boundary-search essential. It teaches why finding one occurrence is not enough. | [Practice](practice/array/29-find-first-and-last-position-of-element-in-sorted-array.md) |
| 30 | [Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/) | [Binary Search On Arrays](patterns/binary-search.md) | Uses index parity to binary search pairs. It teaches how sorted structure can encode position rules. | [Practice](practice/array/30-single-element-in-a-sorted-array.md) |
| 31 | [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) | [Binary Search On Arrays](patterns/binary-search.md), [Heap And Selection](patterns/heap-and-selection.md) | A sorted-array selection problem. It teaches binary searching the best window start. | [Practice](practice/array/31-find-k-closest-elements.md) |
| 32 | [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) | [Binary Search On Answer](patterns/binary-search-on-answer.md) | A classic minimum feasible rate problem. It makes binary search on answer very concrete. | [Practice](practice/array/32-koko-eating-bananas.md) |
| 33 | [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) | [Binary Search On Answer](patterns/binary-search-on-answer.md) | Another strong binary-search-on-answer problem. It teaches how to build the feasibility simulation carefully. | [Practice](practice/array/33-capacity-to-ship-packages-within-d-days.md) |
| 34 | [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls/) | [Binary Search On Answer](patterns/binary-search-on-answer.md), [Sorting-Based Array Patterns](patterns/sorting.md) | This is the maximize-minimum version of binary search on answer. It teaches the opposite movement from minimum feasible problems. | [Practice](practice/array/34-magnetic-force-between-two-balls.md) |
| 35 | [Merge Intervals](https://leetcode.com/problems/merge-intervals/) | [Intervals](patterns/intervals.md), [Sorting-Based Array Patterns](patterns/sorting.md) | The foundational intervals problem. It teaches why sorting by start turns global overlap into local overlap. | [Practice](practice/array/35-merge-intervals.md) |
| 36 | [Insert Interval](https://leetcode.com/problems/insert-interval/) | [Intervals](patterns/intervals.md) | Practices interval merging without sorting because the input is already sorted. It teaches three-phase interval processing. | [Practice](practice/array/36-insert-interval.md) |
| 37 | [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) | [Intervals](patterns/intervals.md), [Greedy Array Decisions](patterns/greedy-arrays.md) | A greedy interval problem. It teaches why sorting by end keeps the most future options open. | [Practice](practice/array/37-non-overlapping-intervals.md) |
| 38 | [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) | [Intervals](patterns/intervals.md), [Greedy Array Decisions](patterns/greedy-arrays.md) | Another end-sorted interval greedy problem. It reinforces choosing a point that covers as many current intervals as possible. | [Practice](practice/array/38-minimum-number-of-arrows-to-burst-balloons.md) |
| 39 | [Gas Station](https://leetcode.com/problems/gas-station/) | [Greedy Array Decisions](patterns/greedy-arrays.md) | A classic reset-greedy scan. It teaches how a failed segment can be discarded completely. | [Practice](practice/array/39-gas-station.md) |
| 40 | [Jump Game](https://leetcode.com/problems/jump-game/) | [Greedy Array Decisions](patterns/greedy-arrays.md) | The core farthest-reach greedy problem. It teaches how one variable can summarize reachability. | [Practice](practice/array/40-jump-game.md) |
| 41 | [Jump Game II](https://leetcode.com/problems/jump-game-ii/) | [Greedy Array Decisions](patterns/greedy-arrays.md) | Extends farthest reach to minimum jumps. It teaches the idea of scanning jump layers. | [Practice](practice/array/41-jump-game-ii.md) |
| 42 | [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) | [Kadane And Subarray Optimization](patterns/kadane.md) | The foundational Kadane problem. It teaches when to continue a subarray and when to restart. | [Practice](practice/array/42-maximum-subarray.md) |
| 43 | [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) | [Kadane And Subarray Optimization](patterns/kadane.md) | A Kadane variant where negative numbers change the state. It teaches why tracking only the best positive product is insufficient. | [Practice](practice/array/43-maximum-product-subarray.md) |
| 44 | [Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/) | [Kadane And Subarray Optimization](patterns/kadane.md) | A deeper Kadane problem. It teaches how circular wrapping can be represented by excluding a minimum middle subarray. | [Practice](practice/array/44-maximum-sum-circular-subarray.md) |
| 45 | [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) | [Monotonic Stack](patterns/monotonic-stack.md) | The standard next-greater-distance problem. It teaches why indexes, not just values, belong on the stack. | [Practice](practice/array/45-daily-temperatures.md) |
| 46 | [Asteroid Collision](https://leetcode.com/problems/asteroid-collision/) | [Monotonic Stack](patterns/monotonic-stack.md) | A stack simulation problem with direction rules. It teaches how to handle repeated conflict against the stack top. | [Practice](practice/array/46-asteroid-collision.md) |
| 47 | [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/) | [Monotonic Stack](patterns/monotonic-stack.md) | Adds circular-array handling to monotonic stack. It teaches the scan-twice trick. | [Practice](practice/array/47-next-greater-element-ii.md) |
| 48 | [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) | [Matrix Array Problems](patterns/matrix.md) | A boundary-control matrix problem. It teaches careful traversal without revisiting cells. | [Practice](practice/array/48-spiral-matrix.md) |
| 49 | [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/) | [Matrix Array Problems](patterns/matrix.md), [In-Place Array Techniques](patterns/in-place-array-techniques.md) | A classic in-place matrix marking problem. It teaches how to use reserved rows and columns as memory. | [Practice](practice/array/49-set-matrix-zeroes.md) |
| 50 | [Rotate Image](https://leetcode.com/problems/rotate-image/) | [Matrix Array Problems](patterns/matrix.md), [In-Place Array Techniques](patterns/in-place-array-techniques.md) | A clean in-place 2D transformation. It teaches how rotation can be decomposed into simpler operations. | [Practice](practice/array/50-rotate-image.md) |

## Pattern Map

- [Two Pointers](patterns/two-pointers.md)
- [Sliding Window](patterns/sliding-window.md)
- [Prefix Sum](patterns/prefix-sum.md)
- [Hashing With Arrays](patterns/hashing.md)
- [Sorting-Based Array Patterns](patterns/sorting.md)
- [Binary Search On Arrays](patterns/binary-search.md)
- [Binary Search On Answer](patterns/binary-search-on-answer.md)
- [Intervals](patterns/intervals.md)
- [Kadane And Subarray Optimization](patterns/kadane.md)
- [Monotonic Stack](patterns/monotonic-stack.md)
- [Matrix Array Problems](patterns/matrix.md)
- [In-Place Array Techniques](patterns/in-place-array-techniques.md)
- [Greedy Array Decisions](patterns/greedy-arrays.md)
- [Heap And Selection](patterns/heap-and-selection.md)
- [Boyer-Moore Voting](patterns/boyer-moore-voting.md)

## Notes

- All solutions in the practice files use Python.
- Problem explanations are paraphrased for learning. Use the LeetCode links for the original prompts and submission.
- Some questions use more than one pattern. In those cases, the practice file explains which pattern does the main work and which pattern supports it.
