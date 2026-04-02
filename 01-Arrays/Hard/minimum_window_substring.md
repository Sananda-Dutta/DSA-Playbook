# 🧩 Minimum Window Substring
## 🧠 Intuition

We need the smallest substring of s containing all characters of t.

## 👉 Key idea:

Use sliding window
Expand window to include all chars
Shrink window to minimize size
## 🐢 Brute Force Approach
Generate all substrings
Check if valid
Track smallest
```cpp
#include <string>
#include <unordered_map>
using namespace std;

bool containsAll(string s, unordered_map<char,int>& mp) {
    unordered_map<char,int> temp;
    for (char c : s) temp[c]++;

    for (auto& it : mp) {
        if (temp[it.first] < it.second) return false;
    }
    return true;
}

string minWindow(string s, string t) {
    int n = s.size();
    unordered_map<char,int> mp;
    for (char c : t) mp[c]++;

    string res = "";

    for (int i = 0; i < n; i++) {
        string temp = "";
        for (int j = i; j < n; j++) {
            temp += s[j];
            if (containsAll(temp, mp)) {
                if (res == "" || temp.size() < res.size()) {
                    res = temp;
                }
                break;
            }
        }
    }

    return res;
}
```
## ⚡ Better Approach (Sliding Window with Maps)
Use frequency maps
Expand + shrink window
## 🚀 Optimal Approach
Use:
need → frequency of t
window → current window frequency
Track:
have → matched characters
required → total unique chars
```cpp
#include <string>
#include <unordered_map>
#include <climits>
using namespace std;

string minWindow(string s, string t) {
    unordered_map<char, int> need, window;

    for (char c : t) need[c]++;

    int have = 0, required = need.size();
    int left = 0;
    int minLen = INT_MAX, start = 0;

    for (int right = 0; right < s.size(); right++) {
        char c = s[right];
        window[c]++;

        if (need.count(c) && window[c] == need[c]) {
            have++;
        }

        while (have == required) {
            if ((right - left + 1) < minLen) {
                minLen = right - left + 1;
                start = left;
            }

            char leftChar = s[left];
            window[leftChar]--;

            if (need.count(leftChar) && window[leftChar] < need[leftChar]) {
                have--;
            }

            left++;
        }
    }

    return minLen == INT_MAX ? "" : s.substr(start, minLen);
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1) (since charset is fixed)
## 🔁 Pattern
Sliding Window
Two Pointer + HashMap
## 🌍 Real World Use
Text search engines (smallest matching substring)
DNA sequence matching
Log analysis (minimum pattern match)
