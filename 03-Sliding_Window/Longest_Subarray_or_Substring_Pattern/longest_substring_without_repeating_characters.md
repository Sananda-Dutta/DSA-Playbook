# 🧩 Longest Substring Without Repeating Characters
## 🧠 Intuition

We need the longest substring with all unique characters.

## 👉 Key idea:

Use sliding window
Expand window until duplicate appears
Shrink from left
## 🐢 Brute Force Approach
Generate all substrings
Check uniqueness
```cpp
#include <string>
#include <unordered_set>
using namespace std;

int lengthOfLongestSubstring(string s) {
    int n = s.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        unordered_set<char> st;
        for (int j = i; j < n; j++) {
            if (st.count(s[j])) break;
            st.insert(s[j]);
            maxLen = max(maxLen, j - i + 1);
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (Sliding Window with Set)
Use set + two pointers
```cpp
#include <string>
#include <unordered_set>
using namespace std;

int lengthOfLongestSubstring(string s) {
    unordered_set<char> st;
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.size(); right++) {
        while (st.count(s[right])) {
            st.erase(s[left]);
            left++;
        }
        st.insert(s[right]);
        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
## 🚀 Optimal Approach (Sliding Window + HashMap)
Store last index of characters
Jump left pointer directly
```cpp
#include <string>
#include <unordered_map>
using namespace std;

int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> mp;
    int left = 0, maxLen = 0;

    for (int right = 0; right < s.size(); right++) {
        if (mp.find(s[right]) != mp.end()) {
            left = max(left, mp[s[right]] + 1);
        }

        mp[s[right]] = right;
        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)
## 🔁 Pattern
Sliding Window
HashMap / Set
## 🌍 Real World Use
Longest unique sequence detection
Data stream analysis
