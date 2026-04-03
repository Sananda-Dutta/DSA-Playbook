# 🧩 Maximum Consecutive Ones
## 🧠 Intuition

We need the longest sequence of continuous 1s.

## 👉 Key idea:

Count consecutive 1s
Reset count when 0 appears
## 🐢 Brute Force Approach
Check all subarrays
Count only those with all 1s
```cpp
#include <vector>
using namespace std;

int findMaxConsecutiveOnes(vector<int>& nums) {
    int n = nums.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = i; j < n; j++) {
            if (nums[j] == 1) {
                count++;
                maxLen = max(maxLen, count);
            } else {
                break;
            }
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (if any)
Not needed → directly optimal
## 🚀 Optimal Approach
Traverse once
Maintain current count and max
```cpp
#include <vector>
using namespace std;

int findMaxConsecutiveOnes(vector<int>& nums) {
    int count = 0, maxLen = 0;

    for (int num : nums) {
        if (num == 1) {
            count++;
            maxLen = max(maxLen, count);
        } else {
            count = 0;
        }
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Linear Traversal
Counting Streak
## 🌍 Real World Use
Finding longest active streak (user activity, uptime)
Binary signal analysis
