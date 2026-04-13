# 🧩 Longest Substring with At Most K Distinct Characters
## 🧠 Intuition

We need the longest substring containing at most K distinct characters.

## 👉 Key idea:

Use sliding window + hashmap
Expand window
Shrink when distinct characters > k
## 🐢 Brute Force Approach
Generate all substrings
Count distinct characters
```cpp
#include <string>
#include <unordered_set>
using namespace std;

int longestKSubstr(string s, int k) {
    int n = s.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        unordered_set<char> st;
        for (int j = i; j < n; j++) {
            st.insert(s[j]);
            if (st.size() <= k) {
                maxLen = max(maxLen, j - i + 1);
            } else break;
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (Sliding Window + Map)
```cpp
#include <string>
#include <unordered_map>
using namespace std;

int longestKSubstr(string s, int k) {
    unordered_map<char, int> mp;
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.size(); right++) {
        mp[s[right]]++;

        while (mp.size() > k) {
            mp[s[left]]--;
            if (mp[s[left]] == 0) {
                mp.erase(s[left]);
            }
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
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
Longest valid segment with limited categories
Resource-constrained streaming
