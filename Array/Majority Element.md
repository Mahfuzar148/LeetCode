

https://leetcode.com/problems/majority-element/solutions/3676530/3-methods-beats-100-c-java-python-beginn-5cy0/

---

# 📘 **Majority Element — বাংলা Documentation**

**Problem:** একটি array দেওয়া আছে। Majority element বলতে বোঝায় —
যে element **n/2 বার এর বেশি** বার এসেছে।
Problem guarantee করে যে majority element **আছেই**।

---

# ✅ **Approach 1: Sorting**

### **💡 Intuition (ভাবনা):**

যদি কোনো সংখ্যা **n/2-এর বেশি** বার আসে,
তাহলে array sort করার পর সেটি **মধ্যের index** (index = n/2) এ থাকা নিশ্চিত।

কারণ majority element এত বেশি বার আসে যে এটি array-র মাঝখানের জায়গা দখল করে।

---

### ✔ **Explanation:**

1. array sort করো
2. sorted array-তে index = `n/2` পজিশনে majority element থাকবে
3. সেটি return করো

---

### ⭐ Code (C++)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
};
```

---

### ⏱ Time Complexity

* Sorting → **O(n log n)**
* Space → **O(1)** (in-place sort)

---

# ✅ **Approach 2: Hash Map (Frequency Count)**

### 💡 **Intuition:**

Hash map দিয়ে array-র প্রতিটি সংখ্যার frequency (কত বার এসেছে) count করা যায়।
যে element-এর count > n/2 হবে, সেটিই majority।

---

### ✔ **Explanation:**

1. একটি hashmap (unordered_map) নাও
2. array এর প্রতিটি element map-এ count বাড়াও
3. যে element-এর count > n/2, সেটি return করো
4. Problem guarantee অনুযায়ী majority থাকবেই

---

### ⭐ Code (C++)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> mp;
        int n = nums.size() / 2;

        for(int x : nums) mp[x]++;

        for(auto &p : mp)
            if(p.second > n)
                return p.first;

        return 0; // theoretically never reached
    }
};
```

---

### ⏱ Time Complexity

* Counting → **O(n)**
* Map size max → n
* Space → **O(n)**

---

# ✅ **Approach 3: Moore’s Voting Algorithm (Best Approach)**

### 💡 **Intuition (সহজ ব্যাখ্যা):**

Majority element সংখ্যাটি array-তে **অন্য সব সংখ্যার চেয়েও বেশি** বার আসে।
তাই pair করে cancel করলে শেষ পর্যন্ত majority element-ই বেঁচে থাকে।

এটা ঠিক ভোটের মতো —
বাকিরা যত ভোট পাক, majority সবসময় লিডে থাকবে।

---

# 📌 Algorithm Steps

1. `candidate = কোন সংখ্যা`, `count = 0`
2. array traverse করো

   * যদি count == 0 → new candidate নাও
   * যদি current element == candidate → count++
   * নাহলে → count--
3. শেষে candidate-এই majority element

---

### ⭐ Code (C++)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0, candidate = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }
        return candidate;
    }
};
```

---

# 🎯 কেন এটা কাজ করে? (বাংলায় বোঝা সহজ)

ধরো majority element = M
এবং অন্যান্য element গুলো = X

Algorithm-এ যখনই X আসে, সেটা M এর একটি ভোট cancel করে।
কিন্তু যেহেতু M আসে মোট n/2 এর বেশি বার,
এ কারণে X যতই আসুক, M সবসময় শেষে লিডে থাকবে।

---

### ⭐ Complexity

* Time → **O(n)** (একবারে scan)
* Space → **O(1)** (কোনো extra memory লাগে না)
* সবচেয়ে efficient / optimal solution

---

# 🔥 Summary Table

| Approach           | Time       | Space | ভালো দিক                                 |
| ------------------ | ---------- | ----- | ---------------------------------------- |
| Sorting            | O(n log n) | O(1)  | সহজ                                      |
| Hash Map           | O(n)       | O(n)  | frequency দেখে দরকার হলে verify করা যায়  |
| **Moore’s Voting** | ⭐O(n)      | ⭐O(1) | Interview-এ সবার favorite, সবচেয়ে দ্রুত |

---

