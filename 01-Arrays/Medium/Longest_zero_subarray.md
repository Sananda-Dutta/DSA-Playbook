# 🧩 Longest Subarray with Sum = 0
## 🧠 Intuition

We need the longest subarray whose sum = 0.

## 👉 Key idea:

Use prefix sum
If same sum appears again → subarray between them = 0
## 🐢 Brute Force Approach
Generate all subarrays
Check sum = 0
Track maximum length
```cpp
#include <vector>
using namespace std;

int maxLen(vector<int>& nums) {
    int n = nums.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum == 0) {
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (if any)
No significant improvement → go optimal
## 🚀 Optimal Approach (Prefix Sum + HashMap)
Store first occurrence of prefix sum
If same sum repeats → subarray sum = 0
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int maxLen(vector<int>& nums) {
    unordered_map<int, int> mp;
    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.size(); i++) {
        sum += nums[i];

        if (sum == 0) {
            maxLen = i + 1;
        }

        if (mp.find(sum) != mp.end()) {
            maxLen = max(maxLen, i - mp[sum]);
        } else {
            mp[sum] = i;
        }
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)
## 🔁 Pattern
Prefix Sum
HashMap
## 🌍 Real World Use
Detecting balanced segments in data
Financial analysis (net-zero transactions)
