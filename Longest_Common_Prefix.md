# 14. Longest Common Prefix

## 📌 Goal

Find the **longest starting substring** common to **all** strings in the array.
If no common prefix exists, return `""`.

---

## 💡 Core Idea (Why Sorting Works)

* Sort the array of strings
* After sorting:

  * The **most different** strings are at the start and end
* If the **first** and **last** strings share a prefix:

  * All middle strings must share it too

So we only compare **two strings**, not all.

---

## 🔁 Algorithm

1. Sort the list of strings
2. Take the first and last strings
3. Compare characters one by one
4. Stop at the first mismatch
5. Return the prefix built so far

---

## 🧠 Python Code (LeetCode Style)

```python
class Solution:
    def longestCommonPrefix(self, v: List[str]) -> str:
        ans = ""
        v = sorted(v)
        first = v[0]
        last = v[-1]

        for i in range(min(len(first), len(last))):
            if first[i] != last[i]:
                return ans
            ans += first[i]

        return ans
```

---

## 🔍 Key Lines Explained

* `v = sorted(v)` → pushes most different strings to the ends
* `first = v[0]`, `last = v[-1]` → only these two matter
* `min(len(first), len(last))` → prevents index overflow
* Mismatch → stop immediately (prefix breaks)

---

## 📘 Example

```
Input: ["flower", "flow", "flight"]
Sorted: ["flight", "flow", "flower"]
Compare: "flight" & "flower"
Output: "fl"
```

---

## ⏱️ Complexity

* **Time:** `O(n log n)` (sorting)
* **Space:** `O(1)` extra (excluding sort)

---

## 🧠 Pattern / Memory Hook

```
Sort → compare ends → build prefix → stop early
```

---
