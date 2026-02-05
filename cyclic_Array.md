
# 🔁 Cyclic Array Transformation (Modulo Indexing)

## 🧠 Problem Idea

You are given an integer array `nums`.

For **each index `i`**:
- Move **forward** if `nums[i] > 0`
- Move **backward** if `nums[i] < 0`
- Wrap around the array **cyclically**
- Set `result[i]` to the value found at the computed index

This problem is all about **circular indexing** and handling **negative modulo correctly**.

---

## 💡 Key Insight

> **Modulo (`%`) turns a linear array into a circle**

But ⚠️ **Java’s `%` can return negative values**, so we must normalize indices.

---

## ✅Algorithm

For every index `i`:

1. Start from `index = i`
2. Shift by `nums[i]`
3. Use modulo `% n` to stay in bounds
4. If index becomes negative → fix it , by normalization -> index += n
5. Assign `result[i] = nums[index]`

---

## 🧩 Implementation (Java)

```java
class Solution {
    public int[] constructTransformedArray(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            int index = i;

            if (nums[i] > 0) {
                index = (index + nums[i]) % n;
            } 
            else if (nums[i] < 0) {
                index = (index + nums[i]) % n;
                if (index < 0) index += n; // normalize negative index
            }

            result[i] = nums[index];
        }
        return result;
    }
}

