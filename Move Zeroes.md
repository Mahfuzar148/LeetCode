

---

# **🟦 283. Move Zeroes — Problem Description**

দেওয়া হয়েছে একটি integer array **nums**।
তোমার কাজ হলো:

### **👉 সব 0-গুলোকে array-এর শেষে পাঠানো**

এবং

### **👉 non-zero elements-এর relative order (ক্রম) বজায় রাখা**

শর্ত:

* **in-place** করতে হবে (অতিরিক্ত array ব্যবহার করা যাবে না)
* Array-এর size পরিবর্তন করা যাবে না

---

## **Example 1**

**Input:**

```
nums = [0,1,0,3,12]
```

**Output:**

```
[1,3,12,0,0]
```

## **Example 2**

**Input:**

```
nums = [0]
```

**Output:**

```
[0]
```

---

# **🟦 Problem Explanation (সহজ ভাষায়)**

তোমাকে array-এর ভিতর থাকা সব শূন্য (0) কে শেষে নিয়ে যেতে হবে।
কিন্তু non-zero সংখ্যা গুলোর ক্রম যেন ঠিক থাকে।

যেমন:

```
[0,1,0,3,12]
```

Non-zero গুলো → `[1,3,12]`
Zero গুলো → `[0,0]`

তাই final result হবে:

```
[1,3,12,0,0]
```

এটা করতে গিয়ে array এর size কমানো বা নতুন array বানানো নিষেধ।

---

# **🟦 All Solution Approaches**

নীচে **সব popular solution** একে একে দেওয়া হলো, with explanation.

---

# ✅ **Solution 1: Optimized Two-Pointer (Official solution)**

**Time:** O(n)
**Space:** O(1)

### ✔ সবচেয়ে বেশি ব্যবহৃত এবং recommended solution

### ✔ Stable order বজায় থাকে

### ✔ In-place কাজ করে

### 📌 Logic:

* প্রথম pointer (`pos`) non-zero element গুলো সামনে রাখবে
* শেষে বাকি জায়গায় zero বসাবে

### 📌 Code:

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int pos = 0;

        for(int x : nums)
            if(x != 0)
                nums[pos++] = x;

        while(pos < nums.size())
            nums[pos++] = 0;
    }
};
```

---

# **⭐ Solution 2: remove + fill (Most Elegant Solution)**

**Time:** O(n)
**Space:** O(1)
**এটিও optimized এবং খুব clean solution (তোমার ব্যবহার করা solution)**

### 📌 remove() কি করে?

* সব non-zero সামনে copy করে
* zero-গুলোকে শেষে “shift করে রেখে দেয়”
* size পরিবর্তন হয় না
* iterator return করে — যেখানে zero শুরু হয়েছে

তারপর `fill()` দিয়ে শেষে zero বসানো হয়।

### 📌 Code:

```cpp
void moveZeroes(vector<int>& nums) {
    auto it = remove(nums.begin(), nums.end(), 0);
    fill(it, nums.end(), 0);
}
```

**📢 Note:**
এটা Two-pointer এর মতোই fast. Clean & short।

---

# ⚠ Solution 3: Swap-based (Not recommended)

**Time:** O(n²)** worst case**
Zero দেখলেই swap → অনেক swap হয়
Performance খারাপ।

---

# ⚠ Solution 4: Extra array (Not allowed)

* Non-zero গুলো নতুন array-তে push
* শেষে zeros add
* কিন্তু extra array ব্যবহার করা যাবে না (in-place condition ভঙ্গ হয়)

---

# **🟩 Final Recommendation**

* **Most readable:** `remove + fill`
* **Most standard (editorial):** Two-pointer
* **Fastest:** দুটোই একই O(n), কোনটাই fast বা slow না।

তোমার লেখা solution একদম perfect optimized.

---

# 🔗 LeetCode Problem Link

**[https://leetcode.com/problems/move-zeroes/description/](https://leetcode.com/problems/move-zeroes/description/)**

---


