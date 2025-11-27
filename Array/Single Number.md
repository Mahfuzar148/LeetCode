

---

# 📘 **Single Number — বাংলা সম্পূর্ণ Documentation**

🔗 **Problem Link:**
[https://leetcode.com/problems/single-number/](https://leetcode.com/problems/single-number/)

---

# 🧩 **Problem Description (Bangla)**

একটি integer array `nums` দেওয়া আছে।
এখানে—

* প্রতিটি element **exactly দুইবার** এসেছে
* কেবলমাত্র **একটি element একবার** এসেছে

তোমাকে সেই **একটি মাত্র unique element** বের করতে হবে যেটি মাত্র একবার আসে।

Guaranteed:
**Array-তে ঠিক ১টি unique number আছে।**

---

# ✨ উদাহরণ

### Input:

```
nums = [4,1,2,1,2]
```

### Output:

```
4
```

কারণ 4 একবার এসেছে, বাকী সব দুইবার।

---

# 🎯 **Goal**

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

---

# ---------------------------------------------

# 🧠 **Approach 1: Hash Map (Not Constant Space)**

**Intuition:**
প্রতিটি element কতবার এসেছে, সেটা একটি map দিয়ে গণনা করো।
যার frequency = 1, সেটিই unique number.

---

## ✔ Explanation

1. একটি `unordered_map<int,int>` নাও
2. array traverse করে প্রতিটি element-এর frequency count করো
3. যেই key-এর frequency = 1 → সেটিই উত্তর

---

## ⭐ Code

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) { 
        unordered_map<int,int> mp;

        for (int x : nums)
            mp[x]++;

        for (auto &p : mp)
            if (p.second == 1)
                return p.first;

        return -1;
    }
};
```

---

## ⏱ Complexity

* Time → **O(n)**
* Space → **O(n)**
  ⬅ অতিরিক্ত space লাগে, তাই optimal নয়।

---

# ---------------------------------------------

# 🧠 **Approach 2: Sorting (Constant Space)**

**Intuition:**
Array sort করলে
যে সংখ্যাগুলো দুইবার আসে — তারা pair আকারে পাশে পাশে থাকে।

Unique number → যেখানে pair mismatch হবে।

---

## ✔ Explanation

1. first sort the array
2. index 1, 3, 5... দিয়ে loop চালাও
3. অবস্থান `i` এবং `i-1` সমান না হলে `i-1`-ই unique

---

## ⭐ Code

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) { 
        sort(nums.begin(), nums.end());

        for (int i = 1; i < nums.size(); i += 2) {
            if (nums[i] != nums[i-1]) 
                return nums[i-1];
        }
        return nums.back();
    }
};
```

---

## ⏱ Complexity

* Time → **O(n log n)**
* Space → **O(1)**
  ➡ মধ্যম মানের সমাধান, কিন্তু optimal নয় (sorting লাগে)

---

# ---------------------------------------------

# 🧠 **Approach 3: Bitwise XOR – Optimal (Best Solution)**

**Intuition:**
XOR এর যাদু:

```
a ^ a = 0
a ^ 0 = a
a ^ b ^ a = b
```

Duplicate elements XOR করলে **একেবারে cancel** হয়ে যায়,
আর unpaired (single) element বেঁচে যায়।

---

## ✔ Explanation

Array-র সব value-কে XOR করলে:

* যা pair তে আছে → XOR = 0 হয়ে মিলিয়ে যাবে
* unique → XOR শেষে ওই সংখ্যাই থাকবে

---

## ⭐ Code

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) { 
        int ans = 0;
        for (int x : nums)
            ans ^= x;
        return ans;
    }
};
```

---

## ⏱ Complexity

* Time → **O(n)**
* Space → **O(1)**
  ➡ **এটাই সবচেয়ে দ্রুত ও optimal সমাধান।**

---

# ---------------------------------------------

# 🧠 **Approach 4: Mathematical Method (SET + SUM Trick)**

**Intuition:**
সব unique element একবার যোগ করে,
তারপর 2 দিয়ে গুণ করে
array-এর total sum বাদ দিলে
সেই single number পাওয়া যায়।

Formula:

```
Single = 2 * (unique elements sum) – (array sum)
```

---

## ✔ Explanation

ধরো unique elements = a1, a2, a3 … ak
Single element = S

Array sum:

```
= 2(a1 + a2 + ... + ak) + S
```

Set sum:

```
= a1 + a2 + ... + ak + S
```

Then:

```
2*set_sum – array_sum = S
```

---

## ⭐ Code

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) { 
        unordered_set<int> st;
        int arraySum = 0;

        for (int x : nums) {
            st.insert(x);
            arraySum += x;
        }

        int setSum = 0;
        for (int x : st) 
            setSum += x;

        return 2 * setSum - arraySum;
    }
};
```

---

## ⏱ Complexity

* Time → **O(n)**
* Space → **O(n)**
  ➡ কাজ করে, কিন্তু constant space নয়।

---

# ---------------------------------------------

# 🏆 **FINAL RECOMMENDATION (Best Method)**

✔ **Bitwise XOR (Approach 3)**

* Fastest: O(n)
* Least space: O(1)
* Easiest to code
* Easy to remember in interviews
* Physics XOR logic → Same cancel, different remain

---

# 🎁 Extra: XOR WHY WORKS (Bangla Mini-Explanation)

* For duplicate numbers:

  ```
  x ^ x = 0
  ```

* For three numbers:

  ```
  a ^ b ^ a = b
  ```

* XOR does not depend on order

  ```
  (a ^ b ^ a) = (a ^ a ^ b) = b
  ```

* তাই pair value বাদ দিয়ে unique বেঁচে যায়

---


