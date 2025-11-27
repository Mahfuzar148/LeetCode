
---

# 📌 **LeetCode 217 — Contains Duplicate **

🔗 **Problem Link:**
[https://leetcode.com/problems/contains-duplicate/](https://leetcode.com/problems/contains-duplicate/)

---

# 🧩 **Problem Description (Bangla + English)**

### **English Version**

You are given an integer array `nums`.
Return **true** if any value appears **at least twice** in the array.
Return **false** if all elements are **distinct**.

### **Bangla Version**

একটি integer array `nums` দেওয়া আছে।
যদি array-এর কোনো মান **দুইবার বা তার বেশি** পাওয়া যায়, তাহলে **true** রিটার্ন করতে হবে।
যদি array-এর **সবগুলো মান আলাদা (distinct)** হয়, তাহলে **false** রিটার্ন করতে হবে।

---

# 📝 Examples

### **Example 1**

**Input:**
`nums = [1,2,3,1]`

**Output:**
`true`

**Explanation:**
এখানে মান `1` দুইবার পাওয়া গেছে (index 0 এবং 3)।

---

### **Example 2**

**Input:**
`nums = [1,2,3,4]`

**Output:**
`false`

**Explanation:**
সব elements আলাদা।

---

# 🧠 **Approach 1: Brute Force (O(n²))**

### **Intuition**

* প্রতিটি element–কে array-এর অন্য সব element-এর সাথে compare করো।
* কোনো duplication পাওয়া গেলে return true।

### **Bangla Explanation**

* প্রথম element টাকে বাকি সবার সাথে মিলিয়ে দেখো।
* তারপর দ্বিতীয়টাকে…
* এভাবে nested loop ব্যবহার করলে সব possible pair check হয়ে যায়।
* কিন্তু time complexity খুব বেশি—**O(n²)**, তাই TLE হতে পারে।

### ❌ **Code (Brute Force - TLE)**

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] == nums[j])
                    return true;
            }
        }
        return false;
    }
};
```

### **Complexity**

* **Time:** O(n²)
* **Space:** O(1)

---

# 🧠 **Approach 2: Sorting (O(n log n))**

### **Intuition**

* Array sort করলে **duplicates গুলো পাশাপাশি আসে**।
* এখন শুধু consecutive elements তুলনা করলেই duplicate পাওয়া যাবে।

### **Bangla Explanation**

* Sort করলে array এর মান ছোট থেকে বড় হয়ে সাজায়।
* একসাথে বসলে only adjacent elements চেক করলেই duplicate detect করা যাবে।

### ✔ Code (Sorting)

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == nums[i - 1])
                return true;
        }
        return false;
    }
};
```

### **Complexity**

* **Time:** O(n log n)
* **Space:** O(1) (in-place sorting)

---

# 🧠 **Approach 3: Hash Set (Optimal - O(n))**

### **Intuition**

* HashSet-এ element insert করার আগে check করি এটি আগেই ছিল কি না।
* যদি থাকে → duplicate
* Hash operations average O(1)

### **Bangla Explanation**

* HashSet-এ element রাখা হলে duplicate খুব দ্রুত ধরা যায়।
* আগেই থাকলে return true, না থাকলে insert।
* একবার scan করলেই answer পাওয়া যায়।

### ⭐ **Best Code (Hash Set)**

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> seen;
        for (int num : nums) {
            if (seen.count(num) > 0)
                return true;
            seen.insert(num);
        }
        return false;
    }
};
```

### **Complexity**

* **Time:** O(n)
* **Space:** O(n)

---

# 🧠 **Approach 4: Hash Map (O(n))**

### **Intuition**

* HashMap দিয়ে count track করি।
* কোনো element এর count ≥ 1 হলে duplicate detect।

### **Bangla Explanation**

* Key = number
* Value = কতবার পাওয়া গেছে
* যখন second time element পাওয়া যাবে, তখনই duplicate নিশ্চিত।

### ✔ Code (Hash Map)

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_map<int, int> seen;
        for (int num : nums) {
            if (seen[num] >= 1)
                return true;
            seen[num]++;
        }
        return false;
    }
};
```

### **Complexity**

* **Time:** O(n)
* **Space:** O(n)

---

# 📌 **Which Approach Should You Use?**

| Approach    | Time         | Space | Recommended? |
| ----------- | ------------ | ----- | ------------ |
| Brute Force | ❌ O(n²)      | O(1)  | No (TLE)     |
| Sorting     | ✔ O(n log n) | O(1)  | Good         |
| HashSet     | ⭐ **O(n)**   | O(n)  | **Best**     |
| HashMap     | ⭐ O(n)       | O(n)  | Good         |

🔹 Most interviewers prefer **HashSet** → fastest + cleanest.

---

