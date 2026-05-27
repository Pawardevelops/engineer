# Array Pattern Study Guide

This folder is now meant to be used like a workbook, not just a list of notes.

The main mistake in DSA study is jumping straight into medium problems before the pattern has become visible. For arrays, most medium questions are not solved by memorizing code. They are solved by recognizing a small number of movement patterns.

Use this order:

```text
array.md
  -> study_guide.md
  -> patterns/<pattern>.md
  -> easy warm-up drills
  -> practice/array/<medium-question>.md
  -> LeetCode submission
```

## How To Study One Pattern

Do not start with the Python solution.

Use this loop:

1. Read the visual mental model.
2. Draw the pointer/window/state movement by hand.
3. Solve the 3 easy warm-up questions.
4. Read one fully worked medium example.
5. Code the medium problem without looking.
6. Compare your code with the provided Python solution.
7. Write down the one decision rule that made the pattern work.

The decision rule is the most important part.

Examples:

```text
Two pointers:
If the sum is too small in a sorted array, move left because only left can increase the sum.

Sliding window:
Expand right to include new data, then shrink left until the window becomes valid again.

Prefix sum:
If current_prefix - previous_prefix = target, then the subarray between them has sum target.
```

## Pattern Learning Order

Study the patterns in this order:

| Order | Pattern | Why This Order |
|---|---|---|
| 1 | [Two Pointers](patterns/two-pointers.md) | Easiest visual movement: left and right indexes. |
| 2 | [Sliding Window](patterns/sliding-window.md) | Builds on two pointers but focuses on contiguous ranges. |
| 3 | [Prefix Sum](patterns/prefix-sum.md) | Solves subarray problems where sliding window breaks. |
| 4 | [Hashing With Arrays](patterns/hashing.md) | Adds memory of previous values or states. |
| 5 | [Sorting](patterns/sorting.md) | Creates order so simpler decisions become possible. |
| 6 | [Binary Search](patterns/binary-search.md) | Uses order to discard half the search space. |
| 7 | [Binary Search On Answer](patterns/binary-search-on-answer.md) | Searches the answer value using a feasibility check. |
| 8 | [Intervals](patterns/intervals.md) | Uses sorting and greedy decisions on ranges. |
| 9 | [Kadane](patterns/kadane.md) | Tracks best subarray ending at the current index. |
| 10 | [Monotonic Stack](patterns/monotonic-stack.md) | Keeps unresolved indexes in useful order. |
| 11 | [Matrix](patterns/matrix.md) | Applies array thinking to rows, columns, and boundaries. |

## What To Draw

Every pattern has a different picture.

### Two Pointers

```text
Sorted array:

index:  0   1   2   3   4   5
value:  1   3   4   6   8   10
        L                   R

sum too small  -> move L right
sum too large  -> move R left
```

### Sliding Window

```text
nums = [2, 1, 5, 1, 3, 2], k = 3

Window 1: [2, 1, 5]        sum = 8
Window 2:    [1, 5, 1]     sum = 7
Window 3:       [5, 1, 3]  sum = 9
Window 4:          [1, 3, 2] sum = 6
```

### Prefix Sum

```text
nums:     [3,  4, -2,  5]
prefix: [0,  3,  7,  5, 10]

sum from index 1 to 3:
prefix[4] - prefix[1]
= 10 - 3
= 7
```

### Binary Search

```text
Search space:

[ possible possible possible | impossible impossible ]
                         ^
                     boundary

Binary search finds the boundary where the answer changes.
```

## When You Feel Stuck

Ask these questions before looking at the solution:

- What is the brute force solution checking repeatedly?
- Can I keep a state so I do not repeat that work?
- Does the answer use a pair, a contiguous range, a prefix, a sorted boundary, or a previous value?
- What move is always safe?
- What candidate gets eliminated after each step?

If you cannot answer "what gets eliminated?", you have not understood the pattern yet.

## External Study Resources

Use these only after reading the local pattern page. They are for a second explanation, not a replacement for solving.

## University-Level Resources

These are higher-value resources from universities or university-backed course material. Use them when you want the deeper reason behind a pattern, not just the LeetCode trick.

| Resource | Best For | Use With These Patterns |
|---|---|---|
| [MIT 6.006: Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) | Core algorithms, data structures, sorting, hashing, binary heaps, and analysis. Includes lecture videos, notes, practice problems, assignments, and quizzes. | Sorting, Hashing, Binary Search, Heap And Selection |
| [MIT 6.046J: Design and Analysis of Algorithms](https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2015/) | More advanced algorithm design: divide and conquer, greedy algorithms, dynamic programming, randomization, and proofs. | Greedy Arrays, Kadane, Binary Search On Answer |
| [Harvard CS50x Week 2: Arrays](https://cs50.harvard.edu/x/weeks/2/) | Beginner-friendly explanation of arrays and memory layout. | Array fundamentals |
| [Harvard CS50x Week 3: Algorithms](https://cs50.harvard.edu/x/weeks/3/) | Searching, binary search, sorting, asymptotic notation, and recursion. | Binary Search, Sorting |
| [Harvard CS50x Week 5: Data Structures](https://cs50.harvard.edu/x/weeks/5/) | Arrays, resizing arrays, linked lists, hash tables, trees, stacks, and queues. | Hashing, In-Place Techniques, Monotonic Stack |
| [Harvard CS50 Business Lecture 2: Data Structures](https://cs50.harvard.edu/business/notes/2/) | Very visual explanation of memory, arrays, trees, and hash tables. | Arrays, Hashing |
| [Princeton Algorithms, 4th Edition Booksite](https://algs4.cs.princeton.edu/home/) | Excellent written material, code, exercises, and lectures for sorting, searching, hash tables, priority queues, and analysis. | Sorting, Hashing, Heap And Selection, Binary Search |
| [UC Berkeley CS61B Spring 2024](https://sp24.datastructur.es/) | Data structures implementation mindset: arrays, lists, maps, sets, trees, heaps, and algorithmic reasoning. | Hashing, Heap And Selection, Matrix, In-Place Techniques |
| [Stanford CS166: Advanced Data Structures](https://web.stanford.edu/class/cs166/) | Advanced structures: range minimum queries, hashing, sketching, heaps, balanced trees, and amortized analysis. | Hashing, Monotonic Stack, Heap And Selection |
| [CMU 15-210: Parallel and Sequential Data Structures and Algorithms](https://www.cs.cmu.edu/~15210/index.html) | Strong theoretical view of sequences, scans, reductions, divide and conquer, greedy methods, hashing, and dynamic programming. | Prefix Sum, Greedy Arrays, Kadane |
| [CMU: Prefix Sums and Their Applications](https://www.cs.cmu.edu/~scandal/papers/CMU-CS-90-190.html) | Deeper paper-style explanation of prefix sums as a general scan operation. | Prefix Sum |

## How To Use University Resources

Do not try to finish a whole MIT or Stanford course before solving problems. Use them surgically.

Recommended mapping:

| If You Are Stuck On | Read Or Watch |
|---|---|
| Why array access is O(1) | Harvard CS50x Week 2 and CS50 Business Lecture 2 |
| Binary search decisions | Harvard CS50x Week 3, then MIT 6.006 |
| Sorting and duplicate handling | Princeton Algorithms Chapter 2 and MIT 6.006 |
| Hash maps and frequency counting | Harvard CS50x Week 5, Princeton Algorithms Chapter 3, MIT 6.006 |
| Heaps and top-k problems | Princeton Priority Queues and MIT 6.006 |
| Prefix sums | CMU prefix sums paper, CMU 15-210 sequence/scan material |
| Greedy proof intuition | MIT 6.046J and CMU 15-210 |
| Advanced data structure intuition | Stanford CS166 |

## Practice And Visual Resources

| Resource | Best For |
|---|---|
| [VisuAlgo](https://visualgo.net/) | Visual algorithm movement and animations. |
| [NeetCode Practice](https://neetcode.io/practice) | Pattern-based problem lists and video explanations. |
| [LeetCode 75](https://leetcode.com/studyplan/leetcode-75/) | Focused interview practice set. |
| [USACO Two Pointers](https://usaco.guide/silver/two-pointers) | Clear two-pointer explanation with competitive-programming examples. |
| [USACO Prefix Sums](https://usaco.guide/silver/prefix-sums) | Strong explanation of prefix sum range queries. |
| [GeeksforGeeks Two Pointers](https://www.geeksforgeeks.org/dsa/two-pointers-technique/) | Beginner-friendly two-pointer article with illustrations. |
| [GeeksforGeeks Binary Search](https://www.geeksforgeeks.org/binary-search-identify-solve-and-interview-questions/) | Binary search identification and examples. |

## Weekly Practice Plan

Use this if the patterns feel confusing.

| Day | Work |
|---|---|
| Day 1 | Two Pointers: read pattern, solve 3 easy drills, then Container With Most Water. |
| Day 2 | Sliding Window: read pattern, solve 3 easy drills, then Minimum Size Subarray Sum. |
| Day 3 | Prefix Sum: read pattern, solve 3 easy drills, then Subarray Sum Equals K. |
| Day 4 | Hashing + Sorting: solve Longest Consecutive Sequence and 3Sum. |
| Day 5 | Binary Search: solve Search in Rotated Sorted Array and Find Minimum. |
| Day 6 | Binary Search On Answer: solve Koko Eating Bananas and Ship Packages. |
| Day 7 | Review only. Redo problems without looking at notes. |

## The Rule For Medium Questions

Before opening a medium question solution, write this:

```text
Pattern:
State I will keep:
What makes the state valid:
When I update the answer:
Why my pointer/search/stack move is safe:
```

If those five lines are clear, the code becomes much easier.
