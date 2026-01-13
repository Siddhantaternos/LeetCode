# 📦 Container With Most Water — Notes

## Problem Summary

Given an array `height` of positive integers representing vertical lines on the x-axis, find two lines that form a container with the **maximum amount of water**.

* You cannot tilt the container
* You must choose two different indices
* Return the maximum possible area

---

## Why This Is a Pattern Problem

This is not about brute force.
It’s about **optimizing space between bars while maximizing the smaller height** — a classic **two-pointer optimization**.

---

## Core Idea (Insight)

At any two pointers ( left ) and ( right ):

[
\text{Area} = \text{width} \times \text{min(height[left], height[right])}
]

* Width = `right - left`
* Height limited by **shorter line**

You want to maximize area by:

* Trying **wide width**
* Increasing the **minimum height**

---

## Pattern Used

👉 **Two Pointers (Greedy)**

* One pointer starts at the beginning
* One pointer starts at the end
* Move the pointer with the **smaller height**

This works because shifting the taller pointer cannot increase the area — only shifting the shorter pointer can potentially increase the boundary height.

---

## Two-Pointer Logic (Why It Works)

1. Start with the **widest possible container**
2. Calculate area
3. Move the pointer with the **smaller height**

   * This is the only move that can possibly increase area
4. Stop when pointers meet

---

## Step-by-Step

```txt
left = 0
right = len(height)-1

maxArea = 0

while left < right:
    width = right - left
    currentHeight = min(height[left], height[right])
    area = width * currentHeight
    update maxArea

    if height[left] < height[right]:
        left += 1
    else:
        right -= 1
```

---

## Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_area = 0

        while left < right:
            width = right - left
            h = min(height[left], height[right])
            max_area = max(max_area, width * h)

            # Move the pointer on the shorter line
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area
```

---

## Complexity

| Metric | Value    |
| ------ | -------- |
| Time   | **O(n)** |
| Space  | **O(1)** |

---

## Mental Model

* Wider containers start better
* Ending pointers are moving toward each other
* The height of the container is **always determined by the smaller line**
* You shift pointers to chase larger minimum heights

---

## Example Walkthrough

Input:

```
height = [1,8,6,2,5,4,8,3,7]
```

The maximum area is formed by lines at positions 1 and 8:

* Width = 8 − 1 = 7
* Height = min(8, 7) = 7
* Area = 49

---

## Interview Signal

If you can explain:

* why we move the **shorter pointer**, not the taller
* why brute–force is too slow (`O(n²)`)
* how this becomes `O(n)`

then you fully *own* this problem.

---

## Pattern Table

| Problem                   | Pattern            |
| ------------------------- | ------------------ |
| Two Sum (sorted)          | Two Pointers       |
| Container With Most Water | Two Pointers       |
| 3Sum                      | Fix + Two Pointers |
| Valid Palindrome          | Two Pointers       |

