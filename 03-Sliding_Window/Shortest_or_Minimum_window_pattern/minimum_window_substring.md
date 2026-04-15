# 🧩 Minimum Window Substring
## 🧠 Intuition

We need the smallest substring that contains all characters of string t.

## 👉 Key idea:

Use sliding window + frequency map
Expand until valid
Shrink to minimize
## 🐢 Brute Force Approach
Check all substrings
Verify if they contain all chars of t
```cpp
#include <string>
#include <unordered_map>
using namespace std;

string minWindow(string s, string t) {
    int n = s.size();
    string res = "";

    for (int i = 0; i < n; i++) {
        unordered_map<char, int> mp;
        for (char c : t) mp[c]++;

        for (int j = i; j < n; j++) {
            if (mp.find(s[j]) != mp.end()) {
                mp[s[j]]--;
                if (mp[s[j]] == 0) mp.erase(s[j]);
            }

            if (mp.empty()) {
                if (res == "" || j - i + 1 < res.size()) {
                    res = s.substr(i, j - i + 1);
                }
                break;
            }
        }
    }

    return res;
}
```
## ⚡ Better Approach (Sliding Window + Map)
## 🚀 Optimal Approach
### Steps:
Store freq of t
Expand window
When valid:
Try shrinking
Update minimum window
```cpp
#include <string>
#include <unordered_map>
#include <climits>
using namespace std;

string minWindow(string s, string t) {
    unordered_map<char, int> mp;
    for (char c : t) mp[c]++;

    int left = 0, count = t.size();
    int minLen = INT_MAX, start = 0;

    for (int right = 0; right < s.size(); right++) {
        if (mp[s[right]] > 0) count--;
        mp[s[right]]--;

        while (count == 0) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                start = left;
            }

            mp[s[left]]++;
            if (mp[s[left]] > 0) count++;
            left++;
        }
    }

    return (minLen == INT_MAX) ? "" : s.substr(start, minLen);
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Minimum Window with Constraints
## 🌍 Real World Use
Smallest segment containing required data
Text search / pattern matching
