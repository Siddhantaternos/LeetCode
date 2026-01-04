# Remove Duplicates from Sorted Array

## 📌 Problem

Given a **sorted** array `nums`, remove duplicates **in-place** such that each unique element appears only once.

Return the number of unique elements `k`.

* The first `k` elements of `nums` must contain the unique values
* Elements after index `k - 1` do **not matter**

---

## 📊 Constraints

* Array is **sorted**
* In-place modification (no extra array)

---

## 💡 Core Idea

Use **two pointers**:

* One pointer **reads** elements
* One pointer **writes** unique elements

Instead of deleting duplicates, **overwrite them**.

---

## 🔁 Algorithm

1. First element is always unique → set `k = 1`
2. Loop from index `1` to end
3. If current element ≠ previous element:

   * Write it at index `k`
   * Increment `k`
4. Return `k`

---

## 🧠 Python Code (LeetCode Style)

```python
class Solution:
    def removeDuplicates(self, nums):
        if not nums:
            return 0

        k = 1
        for i in range(1, len(nums)):
            if nums[i] != nums[i - 1]:
                nums[k] = nums[i]
                k += 1
        return k
```

---

## 🔍 Example

**Input**

```
nums = [0,0,1,1,2,2,3]
```

**Output**

```
k = 4
nums = [0,1,2,3,_,_,_]
```

Only the first `k` elements are valid.

---

## ⏱️ Time & Space

* **Time:** `O(n)`
* **Space:** `O(1)`

---

## 🧩 Key Concepts Used

* Lists & indexing
* `for` loop
* `if` condition
* In-place modification
* Sorted array property

---

## 🧠 Pattern Name

👉 **Two Pointer Technique (Slow–Fast Pointer)**

---
