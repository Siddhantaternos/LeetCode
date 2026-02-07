# 🔢 Next Permutation — Notes

## 📌 Problem Summary

Given an integer array `nums`, rearrange it into the **next lexicographically greater permutation**.
If such arrangement is not possible, rearrange it into the **lowest possible order** (i.e., sorted ascending).

You must modify `nums` **in-place**, with only constant extra memory.

---

## 🧠 Core Insight

A permutation’s **next lexicographic order** means:

> The **smallest change** that makes the sequence **just greater** than the current one.

Think of permutations as words ordered lexicographically:

```
123 → 132 → 213 → 231 → 312 → 321
```

---

## 🔑 Key Steps (Pattern)

1. Find the **first decreasing element** from the right (call its index `i`)
2. If none exists → the permutation is the **highest** → reverse entire array
3. Otherwise, find the **smallest number greater than `nums[i]`** to the right (index `j`)
4. Swap `nums[i]` and `nums[j]`
5. Reverse the subarray to the right of `i`

This ensures:

* We make the **smallest upward change**
* The suffix is the **lowest possible order**

---

## 📍 Step-by-Step with Intuition

### 1. Find the Pivot

From right to left, identify the first index `i` such that:

```
nums[i] < nums[i+1]
```

If no such `i`: the entire array is descending → **reverse → done**.

---

### 2. Find the Right Replacement

Looking from the array’s end, find `j` such that:

```
nums[j] > nums[i]
```

Because the suffix is descending, the first such `j` you find is the **smallest greater element**.

---

### 3. Swap and Fix Suffix

Swap elements at `i` and `j`.

The suffix after index `i` is still descending, so reverse it to get the **smallest ascending order**.

---

## 🧠 Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        n = len(nums)
        i = n - 2

        # 1. Find the first decreasing element
        while i >= 0 and nums[i] >= nums[i + 1]:
            i -= 1

        if i >= 0:
            # 2. Find element just larger than nums[i]
            j = n - 1
            while nums[j] <= nums[i]:
                j -= 1

            # 3. Swap
            nums[i], nums[j] = nums[j], nums[i]

        # 4. Reverse the suffix
        left, right = i + 1, n - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

---

## 🔍 Example

Input:

```
nums = [1, 2, 3]
```

Process:

* Pivot at `i = 1` (value `2`)
* Find just greater → `j = 2` (value `3`)
* Swap → `[1, 3, 2]`
* Reverse suffix after pivot → remains `[1, 3, 2]`

Output:

```
[1, 3, 2]
```

---

## ⏱️ Complexity

| Metric | Value    |
| ------ | -------- |
| Time   | **O(n)** |
| Space  | **O(1)** |

---

## 🧠 Why This Works (Key Insight)

The suffix after the pivot is **strictly descending**.
Swapping with the smallest number just bigger than the pivot ensures the next smallest whole sequence.
Reversing the suffix makes it the **lowest possible tail**.

---

## 🧩 Interview Signals

If you can explain:

* Why we scan from the right
* How pivot is chosen
* Why the suffix is reversed
* Why this achieves the next lexicographic permutation

then you truly understand this pattern.

---

## 📌 Pattern Family

This problem belongs to:

* Permutation ordering
* In-place transformation
* Lexicographic sequence logic

---
