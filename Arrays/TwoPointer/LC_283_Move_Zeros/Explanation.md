# 283. Move Zeroes

**Difficulty:** Easy
**Pattern:** Two Pointers (Read/Write Pointer)
**Link:** https://leetcode.com/problems/move-zeroes/

---

## Problem

Given an array `nums`, move all `0`s to the end of it, while keeping the order of the non-zero numbers the same. Do this **in-place** — don't make a new array.

**Example:**
```
Input:  [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
```

---

## Why this pattern? (Two Pointers)

Whenever a question asks you to:
- rearrange an array **in-place**
- **keep the order** of some elements
- split the array into two groups based on a condition (here: zero / non-zero)

...that's a strong signal to use **two pointers**.

One pointer keeps track of *where the next good element should go*. The other pointer just walks through the array checking each element. This way we never need extra space, and we only touch the array once.

---

## How it works

We use two pointers:

- `left` → points to the position where the next **non-zero** number should be placed
- `right` → scans through the array one element at a time

**Logic:**
- If `nums[right]` is **not zero** → swap it with `nums[left]`, then move `left` forward
- If `nums[right]` **is zero** → do nothing, just move `right` forward

**Why swap and not just overwrite?**
Overwrite only moves the non-zero value forward — it doesn't put anything back where that value came from. Swap does both at once: the non-zero moves forward, and the zero takes its old spot. Nothing gets lost, no cleanup needed later.

---

## Dry Run

`nums = [0, 1, 0, 3, 12]`

| i | nums[i] | Is it non-zero? | Action | left (after) | Array after this step |
|---|---------|------------------|--------|----|------------------------|
| 0 | 0  | No  | do nothing | 0 | [0, 1, 0, 3, 12] |
| 1 | 1  | Yes | swap(nums[1], nums[0]), left++ | 1 | [1, 0, 0, 3, 12] |
| 2 | 0  | No  | do nothing | 1 | [1, 0, 0, 3, 12] |
| 3 | 3  | Yes | swap(nums[3], nums[1]), left++ | 2 | [1, 3, 0, 0, 12] |
| 4 | 12 | Yes | swap(nums[4], nums[2]), left++ | 3 | [1, 3, 12, 0, 0] |

**Final array:** `[1, 3, 12, 0, 0]` ✅

---

## Code

```python
def moveZeroes(nums):
    left = 0  # next position for a non-zero number
    for i in range(len(nums)):
        if nums[i] != 0:
            nums[left], nums[i] = nums[i], nums[left]
            left += 1
```

---

## Complexity

- **Time:** O(n) — we go through the array once
- **Space:** O(1) — no extra array used, everything happens in-place

---

## One-line takeaway (for revision)

> Splitting an array in-place while keeping order = two pointers. One pointer marks "where the next good element goes," the other scans. Swap instead of overwrite when both groups need to stay in the array.