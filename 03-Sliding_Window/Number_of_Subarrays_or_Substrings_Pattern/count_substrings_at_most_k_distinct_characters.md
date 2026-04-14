# 🧩 Count Substrings with At Most K Distinct Characters
## 🧠 Intuition

We need number of substrings with at most K distinct characters.

👉 Same logic as subarrays — but applied to strings

## 🐢 Brute Force Approach
Generate all substrings
Count distinct characters
```cpp
#include <string>
#include <unordered_set>
using namespace std;

int countSubstrings(string s, int k) {
    int n = s.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        unordered_set<char> st;
        for (int j = i; j < n; j++) {
            st.insert(s[j]);
            if (st.size() <= k) count++;
            else break;
        }
    }

    return count;
}
```
## ⚡ Better Approach (Sliding Window + Map)
```cpp
#include <string>
#include <unordered_map>
using namespace std;

int countSubstrings(string s, int k) {
    unordered_map<char, int> mp;
    int left = 0, count = 0;

    for (int right = 0; right < s.size(); right++) {
        mp[s[right]]++;

        while (mp.size() > k) {
            mp[s[left]]--;
            if (mp[s[left]] == 0) {
                mp.erase(s[left]);
            }
            left++;
        }

        count += (right - left + 1);
    }

    return count;
}
```
## 🚀 Optimal Approach
Same as above
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(k)
## 🔁 Pattern
Sliding Window
At Most K Distinct
## 🌍 Real World Use
Text analytics (limited vocabulary segments)
Pattern extraction in strings
