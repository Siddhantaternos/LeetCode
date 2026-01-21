# 📍 Search in Rotated Sorted Array

## 🎯 Problem Summary

Given a **rotated sorted array** `nums` (no duplicates) and an integer `target`, return the **index** of `target` in the array.
If `target` is not in the array, return `-1`.

The array was originally sorted in **ascending order** and then rotated at some unknown pivot.

Examples:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

---

## 🧠 Core Idea

The rotated array consists of **two ascending sorted subarrays**.

We leverage this to run a **modified binary search**:

* Use standard binary search framework (`O(log n)`)
* Identify which half (left or right) is sorted
* Restrict search to the half that **could contain the target**

---

## 🔍 Observations

1. At any step:

   * One half (left or right) of the current segment is sorted
2. If `target` lies within the sorted half → search it
3. Otherwise → search the other half

This preserves **logarithmic time**.

---

## 🔁 Algorithm (High-Level)

```
left = 0
right = n - 1

while left <= right:
    mid = (left + right) // 2

    if nums[mid] == target:
        return mid

    if left half sorted (nums[left] <= nums[mid]):
        if target is in [nums[left], nums[mid]):
            narrow to left half
        else:
            go to right half
    else: (right half sorted)
        if target in (nums[mid], nums[right]]:
            narrow to right half
        else:
            go to left half

return -1
```

---

## 🧠 Why This Works

Binary search normally assumes a **fully sorted array**.
In a rotated array, although the whole is not sorted, **one of the two halves always is**.

By detecting which half is sorted, we can decide where to continue the search.

---

## 🧩 Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            # Found target
            if nums[mid] == target:
                return mid

            # Left half is sorted
            if nums[left] <= nums[mid]:
                # Target is in the sorted left half
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            # Right half is sorted
            else:
                # Target is in the sorted right half
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
```

---

## ⏱️ Complexity

| Metric    | Value      |
| --------- | ---------- |
| **Time**  | `O(log n)` |
| **Space** | `O(1)`     |

---

## 🧠 Pattern / Memory Hook

```
Binary search + check sorted half → decide direction
```

---

## 📌 Interview Key Points

If you can explain:

* How to detect which half is sorted
* Why this maintains binary-search complexity
* How bounds contract based on target position

you clearly *own* this problem.

---

## 🧩 Edge Cases

* Single-element array
* Target not present
* Rotation at start or end
* All elements unique (as given)

---

## 🧠 Visualization

```
Indices:   0   1   2   3   4   5   6
nums =   [4   5   6   7   0   1   2]
              ↑
           mid here

Left half is sorted → check target range
Else → right half
```

---
