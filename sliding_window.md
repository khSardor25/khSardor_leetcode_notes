# Sliding Window — Compact Notes

## 1️⃣ When to Use

Use Sliding Window when:

-   Problem involves **contiguous subarray/substring**
    
-   You need **O(n)** instead of **O(n²)**
    
-   Condition depends on window elements (sum, freq, distinct, etc.)
    

----------

# Core Idea

Maintain:

int  left  =  0;  
for (int  right  =  0; right  <  n; right++) {  
  // expand window  
  add(nums[right]);  
  
  // shrink if needed  
  while (invalid) {  
  remove(nums[left]);  
  left++;  
 }  
  
  // update answer  
}

----------

# 2️⃣ Fixed Size Window (size = k)

### Use when:

Window size is constant.

### Template

int  left  =  0;  
int  window  =  0;  
int  best  =  0;  
  
for (int  right  =  0; right  <  n; right++) {  
  window  +=  nums[right];  
  
  if (right  -  left  +  1  ==  k) {  
  best  =  Math.max(best, window);  
  
  window  -=  nums[left];  
  left++;  
 }  
}

⏱ Time: O(n)

----------

# 3️⃣ Variable Size Window

## A) Longest Valid Window (At Most K)

### Pattern:

Shrink when invalid.

int  left  =  0, best  =  0;  
  
for (int  right  =  0; right  <  n; right++) {  
  add(nums[right]);  
  
  while (!valid()) {  
  remove(nums[left]);  
  left++;  
 }  
  
  best  =  Math.max(best, right  -  left  +  1);  
}

Used for:

-   Longest substring without repeating
    
-   At most K distinct
    
-   At most K zeros
    
-   Sum ≤ target (non-negative only)
    

----------

## B) Shortest Valid Window (At Least K)

### Pattern:

Shrink while valid.

int  left  =  0;  
int  best  =  Integer.MAX_VALUE;  
  
for (int  right  =  0; right  <  n; right++) {  
  add(nums[right]);  
  
  while (valid()) {  
  best  =  Math.min(best, right  -  left  +  1);  
  remove(nums[left]);  
  left++;  
 }  
}

Used for:

-   Min subarray sum ≥ target
    
-   Minimum window substring
    

----------

# 4️⃣ Frequency Map Template (Strings)

Map<Character, Integer> map  =  new  HashMap<>();  
int  left  =  0, best  =  0;  
  
for (int  right  =  0; right  <  s.length(); right++) {  
  char  c  =  s.charAt(right);  
  map.put(c, map.getOrDefault(c, 0) +  1);  
  
  while (map.get(c) >  1) {  
  char  d  =  s.charAt(left);  
  map.put(d, map.get(d) -  1);  
  left++;  
 }  
  
  best  =  Math.max(best, right  -  left  +  1);  
}

----------
# 5️⃣ EXACT K Trick

exactly(K) = atMost(K) - atMost(K - 1)

Very common for:

-   Subarrays with K distinct
    
-   Subarrays with K odd numbers
    

----------

# 6️⃣ When Sliding Window Fails

❌ Negative numbers in sum problems  
❌ Non-contiguous requirement  
❌ Order-independent subsets

----------




