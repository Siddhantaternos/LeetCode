# 27. Remove Element — Clean Notes

## Goal

Remove all occurrences of `val` **in-place** from array `nums`.

Return `k` = number of elements **not equal** to `val`.

Only the **first `k` elements matter**.
Order **does not matter**.

---

## Core Constraint (Very Important)

* You **cannot create a new array**
* You must **modify `nums` directly**
* Elements after index `k-1` are **ignored**

This is an **in-place array problem**.

---

## Core Idea

Use a **write pointer** to overwrite unwanted values.

Instead of deleting elements:

* **Skip `val`**
* **Copy valid elements forward**

---

## Algorithm (Two Pointer – Slow/Fast)

* `i` → reads every element
* `k` → writes only valid elements

### Steps

1. Initialize `k = 0`
2. Loop through array with `i`
3. If `nums[i] != val`

   * write `nums[i]` to `nums[k]`
   * increment `k`
4. Return `k`

---

## Code (LeetCode Format)

```python
class Solution:
    def removeElement(self, nums, val):
        k = 0  # write pointer

        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]  # overwrite unwanted values
                k += 1

        return k
```

---

## Example Walkthrough

### Input

```
nums = [3,2,2,3]
val = 3
```

### Process

```
skip 3
keep 2 → nums[0]
keep 2 → nums[1]
skip 3
```

### Result

```
k = 2
nums = [2,2,_,_]
```

---

## Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(1)  |

---

## Pattern Name

👉 **Two Pointer (Overwrite Pattern)**
Also used in:

* Remove Duplicates
* Move Zeroes
* Partition Arrays

---

## Mental Model (Remember This)

> “Don’t remove elements.
> Overwrite the bad ones.”

If you understand this line, you understand the problem.

