# 🧩 Count Subarrays with At Most K Distinct Integers
## 🧠 Intuition

We need to count subarrays having at most K distinct elements.

## 👉 Key idea:

Use sliding window + hashmap
For each right, count valid subarrays ending at right
Add (right - left + 1)
## 🐢 Brute Force Approach
Generate all subarrays
Count distinct elements
```cpp
#include <vector>
#include <unordered_set>
using namespace std;

int countSubarrays(vector<int>& nums, int k) {
    int n = nums.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        unordered_set<int> st;
        for (int j = i; j < n; j++) {
            st.insert(nums[j]);
            if (st.size() <= k) count++;
            else break;
        }
    }

    return count;
}
```
## ⚡ Better Approach (Sliding Window + Map)
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int countSubarrays(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    int left = 0, count = 0;

    for (int right = 0; right < nums.size(); right++) {
        mp[nums[right]]++;

        while (mp.size() > k) {
            mp[nums[left]]--;
            if (mp[nums[left]] == 0) {
                mp.erase(nums[left]);
            }
            left++;
        }

        count += (right - left + 1);
    }

    return count;
}
```
## 🚀 Optimal Approach
Same as above (already optimal)
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(k)
## 🔁 Pattern
Sliding Window
At Most K Distinct
## 🌍 Real World Use
Counting valid segments with limited categories
Streaming analytics
