# 🧹 Minimum Remove to Make Valid Parentheses — Notes

---

## 📌 Problem Goal

Given a string containing:

* `(`
* `)`
* lowercase letters

Remove the **minimum number of parentheses** so the string becomes **valid**.

Valid means:

* Every `(` has a matching `)`
* Order must be correct

---

## 🧠 Core Insight

You are **not checking validity**.
You are **fixing the string with minimum removals**.

That changes the mindset completely.

---

## 💡 Best Approach

👉 Use **Stack (Indices Storage)**

Why indices?
Because you must:

* Track where invalid brackets exist
* Remove them later while building final string

If you only counted → you couldn’t rebuild final string properly.

Reddit engineers often explain it like this:

> Track indices of unmatched brackets using stack
> Remove leftover ones while building final string ([Reddit][1])

---

## 🔁 Algorithm Flow

### Step 1 — Scan string

* If `(` → push index to stack
* If `)`:

  * If stack has `(` → pop (matched pair)
  * Else → mark this index invalid

### Step 2 — After scan

Stack still has unmatched `(` → mark them invalid

### Step 3 — Build result string

Skip all invalid indices

---

## 🧠 Mental Model

```
Scan → Match pairs → Mark invalid → Rebuild string
```

---

## 🧾 Python Code (LeetCode Ready)

```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack = []              # stores indices of '('
        remove = set()          # stores indices to remove

        # Pass 1: find invalid parentheses
        for i, ch in enumerate(s):
            if ch == '(':
                stack.append(i)
            elif ch == ')':
                if stack:
                    stack.pop()
                else:
                    remove.add(i)

        # Any leftover '(' are invalid
        while stack:
            remove.add(stack.pop())

        # Pass 2: build result
        res = []
        for i, ch in enumerate(s):
            if i not in remove:
                res.append(ch)

        return "".join(res)
```

---

## 📘 Example

Input:

```
"a)b(c)d"
```

Process:

```
Remove index of extra ')'
```

Output:

```
"ab(c)d"
```

---

## ⏱️ Complexity

| Type  | Complexity |
| ----- | ---------- |
| Time  | O(n)       |
| Space | O(n)       |

---

## 🧩 Pattern Category

👉 Stack + String Reconstruction
👉 Valid Parentheses Family
👉 Greedy Removal

---

## 🚩 Interview Signals

If you:

* Use stack of **indices** → Strong understanding
* Only count parentheses → Weak solution

Because real interviews test **string rebuilding logic**.

---

## 🧬 Pattern Relatives

| Problem                    | Pattern          |
| -------------------------- | ---------------- |
| Valid Parentheses          | Stack validation |
| Remove Invalid Parentheses | BFS + pruning    |
| Min Add to Make Valid      | Counter          |

---

## 🧠 Deep Insight (The Real Trick)

The hard part isn’t parentheses.
The hard part is:

👉 Tracking structure
👉 Preserving order
👉 Removing minimum

That’s basically 70% of real production string cleanup problems.

---

