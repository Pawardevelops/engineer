# 01. Container With Most Water

## Links

- LeetCode: [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- Pattern: [Two Pointers](../../patterns/two-pointers.md)
- Back to index: [Array Questions](../../array_questions.md)

## Problem In Simple Words

Given heights of vertical lines, choose two lines that hold the most water with the x-axis. The area is width times the shorter height.

The important skill is to identify what the array is really asking you to control: indexes, a window, a running state, sorted order, or an in-place transformation.

## Why This Pattern Fits

The two outermost lines give maximum width first. Since area is limited by the shorter line, moving the taller line inward only loses width without improving the limiting height.

This matters because the optimized solution is not just faster by accident. It is faster because the pattern gives us a rule for safely ignoring work that cannot improve the answer.

## Visual Explanation

Example:

```text
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]

index:   0  1  2  3  4  5  6  7  8
height:  1  8  6  2  5  4  8  3  7
         L                       R
```

The area between `L` and `R` is:

```text
width = R - L
height = min(height[L], height[R])
area = width * height
```

At the start:

```text
L = 0, R = 8
width = 8
min height = min(1, 7) = 1
area = 8
```

The left wall is shorter. That means the current area is limited by `height[L] = 1`.

If we keep `L` and move `R` left:

```text
width gets smaller
limiting height is still at most 1 unless a taller left wall is chosen
```

So keeping the shorter wall cannot help. The only move that can possibly improve the answer is:

```text
move L right
```

This is the whole reason two pointers works here.

## Brute Force Thinking

Try every pair of lines and compute its area. That proves the answer definition clearly, but it checks O(n^2) pairs.

Brute force is still worth understanding first because it defines the answer clearly. Once you know exactly what brute force checks, the optimized pattern is easier to trust.

## Optimized Intuition

The optimized idea is to keep only the state that can still affect the final answer.

For this problem:

- The current state tells us what candidates are still possible.
- The update rule removes candidates that are now impossible or already handled.
- The answer is updated only when the state represents a valid candidate.

## Step-By-Step Algorithm

1. Start left at 0 and right at n - 1.
2. Compute area using the current width and shorter height.
3. Update the best area.
4. Move the pointer at the shorter height because that is the bottleneck.
5. Stop when the pointers meet.

## Dry Run

Input:

```text
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
```

| Step | left | right | width | min height | area | best | Move | Why |
|---|---:|---:|---:|---:|---:|---:|---|---|
| 1 | 0 | 8 | 8 | 1 | 8 | 8 | left++ | Left wall is shorter. |
| 2 | 1 | 8 | 7 | 7 | 49 | 49 | right-- | Right wall is shorter. |
| 3 | 1 | 7 | 6 | 3 | 18 | 49 | right-- | Right wall is shorter. |
| 4 | 1 | 6 | 5 | 8 | 40 | 49 | right-- | Equal height, moving either is safe. |
| 5 | 1 | 5 | 4 | 4 | 16 | 49 | right-- | Right wall is shorter. |
| 6 | 1 | 4 | 3 | 5 | 15 | 49 | right-- | Right wall is shorter. |
| 7 | 1 | 3 | 2 | 2 | 4 | 49 | right-- | Right wall is shorter. |
| 8 | 1 | 2 | 1 | 6 | 6 | 49 | right-- | Right wall is shorter. |

Final answer:

```text
49
```

## Python Solution

```python
from typing import List


class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        best = 0

        while left < right:
            width = right - left
            best = max(best, width * min(height[left], height[right]))

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return best
```

## Line-By-Line Explanation

```text
left, right = 0, len(height) - 1
```

Start with the widest possible container.

```text
width = right - left
best = max(best, width * min(height[left], height[right]))
```

Calculate the current container and keep the largest area seen.

```text
if height[left] < height[right]:
    left += 1
else:
    right -= 1
```

Move the shorter wall because the shorter wall limits the area. Moving the taller wall would only reduce width while keeping the same limiting wall.

## Complexity Analysis

Time O(n), space O(1).

## Common Mistakes

- Moving the taller pointer.
- Forgetting width is right - left.
- Stopping after one local increase instead of scanning until pointers meet.

## What You Should Learn

You learn how a pointer move can be justified by eliminating dominated choices.
