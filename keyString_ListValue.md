
# LeetCode 49 — Group Anagrams

Today I solved an interesting problem on **LeetCode** — **Problem 49: Group Anagrams**.

The core idea of this problem is to **group strings that are anagrams** of each other and return them as a list of lists.

I used an elegant approach where:

- The **key** is the **sorted version of the string**
- The **value** is a **list of all strings that match that key**

This works because all anagrams become identical after sorting their characters.

---

## 🔑 Key Insight

If two words are anagrams, their sorted versions are the same.

Example:
"eat" → "aet"  
"tea" → "aet"  
"tan" → "ant"


So `"aet"` and `"ant"` can be used as keys in a map.

---

Time & Space Complexity

-   **Time Complexity:** `O(n · k log k)`  
    `n` = number of strings, `k` = average length of each string
    
-   **Space Complexity:** `O(n · k)`


## 💻 Java Implementation

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();

        for (String word : strs) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sortedWord = new String(chars);

            map.computeIfAbsent(sortedWord, k -> new ArrayList<>()).add(word);
        }

        return new ArrayList<>(map.values());
    }
}



