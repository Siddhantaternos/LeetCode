# Concatenation of Array

## 📌 Problem

Given an integer array `nums`, return an array `ans` where:

```
ans = nums + nums
```

The new array should contain the original array **twice**, in order.

---

## 💡 Core Idea

* Let `n` be the length of `nums`
* Create a new array of size `2n`
* Copy `nums` into:

  * the **first half**
  * the **second half**

---

## 🔁 Algorithm

1. Get the length `n`
2. Create an array `ans` of size `2 * n`
3. Loop from `0` to `n - 1`
4. Place:

   * `nums[i]` at index `i`
   * `nums[i]` at index `i + n`
5. Return `ans`

---

## 🧠 Python Code (LeetCode Style)

```python
class Solution:
    def getConcatenation(self, nums):
        n = len(nums)
        ans = [0] * (2 * n)

        for i in range(n):
            ans[i] = nums[i]
            ans[i + n] = nums[i]

        return ans
```

---

## 🔍 Example

```
Input: nums = [1, 2, 1]
Output: [1, 2, 1, 1, 2, 1]
```

---

## ⏱️ Complexity

* **Time:** `O(n)`
* **Space:** `O(n)`

---

## 🧩 Key Concepts Used

* Lists
* Indexing
* Looping
* Array size manipulation

---

## 🧠 Pattern / Memory Hook

```
New array → double size → copy twice
```

---
