
# Sliding Window 🪟🔥

Sliding Window is a **core algorithmic technique** used to optimize problems involving  
**subarrays / substrings** from **O(n²)** ➜ **O(n)** ⚡

---

## When to Use 🤔

Keywords that strongly suggest Sliding Window:
- 🧩 subarray / substring
- 🔁 continuous
- 📏 longest / shortest
- 📈 max / min
- 🎯 at most / at least

---

## Core Idea 🧠

Maintain a window `[left → right]`:
- ➕ expand → `right++`
- ➖ shrink → `left++`
- 📝 update result while iterating

---

## Time & Space Complexity
- Time O(N)
- Space O(1)



## Types 🪟

### 1️⃣ Fixed Size Window
Window size = `k`

```java
int sum = 0;
for (int i = 0; i < k; i++) sum += nums[i];

int max = sum;
for (int i = k; i < nums.length; i++) {
    sum += nums[i];
    sum -= nums[i - k];
    max = Math.max(max, sum);
}

