# 🧩 Fruits Into Baskets
## 🧠 Intuition

We need the longest subarray with at most 2 distinct elements.

## 👉 Key idea:

Sliding window with at most 2 types
Expand window, shrink when >2 types
## 🐢 Brute Force Approach
Generate all subarrays
Check distinct count ≤ 2
```cpp
#include <vector>
#include <set>
using namespace std;

int totalFruit(vector<int>& fruits) {
    int n = fruits.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        set<int> st;
        for (int j = i; j < n; j++) {
            st.insert(fruits[j]);
            if (st.size() > 2) break;
            maxLen = max(maxLen, j - i + 1);
        }
    }

    return maxLen;
}
```
##  Better Approach (Sliding Window + Map)
Use hashmap to track frequency
## 🚀 Optimal Approach
Steps:
Expand window
If more than 2 types → shrink
Track max length
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int totalFruit(vector<int>& fruits) {
    unordered_map<int, int> mp;
    int left = 0, maxLen = 0;

    for (int right = 0; right < fruits.size(); right++) {
        mp[fruits[right]]++;

        while (mp.size() > 2) {
            mp[fruits[left]]--;
            if (mp[fruits[left]] == 0) {
                mp.erase(fruits[left]);
            }
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1) (at most 2 types)
## 🔁 Pattern
Sliding Window
At Most K Distinct Elements
## 🌍 Real World Use
Resource allocation with constraints
Longest valid segment detection
