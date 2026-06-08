
# 🧩 LeetCode 12 — Integer to Roman

Today I solved an interesting problem on **LeetCode**:  
**Integer → Roman (Problem #12)**.

One very useful trick I discovered was iterating through a `HashMap` (or `LinkedHashMap`) using `entrySet()`.

This approach lets you access **both keys and values** at the same time — which is perfect for greedy algorithms like Roman numeral conversion.

---

## 🔁 Iterating Through a Map Using `entrySet()`

```java
for (Map.Entry<Integer, String> entry : myMap.entrySet()) {
    int key = entry.getKey();
    String str = entry.getValue();

    System.out.println("Key: " + key + " Value: " + str);
}
```


In python if you are aiming to get both index and value (from the array/list) use enumerate function - this will give you both index and num simultaneously
```python
for i, num in enumerate(nums):
    total += num
    if i % 2 == 0:
        total -= 2

