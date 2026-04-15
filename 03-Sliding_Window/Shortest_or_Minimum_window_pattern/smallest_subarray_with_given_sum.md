# 🧩 Smallest Subarray with Given Sum (Positive Integers)
## 🧠 Intuition

We need the minimum length subarray with sum ≥ target.

## 👉 Key idea:

Since all numbers are positive → use sliding window
## 🐢 Brute Force Approach
Generate all subarrays
Check sum ≥ target
```cpp
#include <vector>
#include <climits>
using namespace std;

int minSubArrayLen(int target, vector<int>& nums) {
    int n = nums.size();
    int minLen = INT_MAX;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum >= target) {
                minLen = min(minLen, j - i + 1);
                break;
            }
        }
    }

    return (minLen == INT_MAX) ? 0 : minLen;
}
```
## ⚡ Better Approach (if any)
Not needed → directly optimal
## 🚀 Optimal Approach (Sliding Window)
Steps:
Expand window
While sum ≥ target:
Update answer
Shrink window
```cpp
#include <vector>
#include <climits>
using namespace std;

int minSubArrayLen(int target, vector<int>& nums) {
    int left = 0, sum = 0;
    int minLen = INT_MAX;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];

        while (sum >= target) {
            minLen = min(minLen, right - left + 1);
            sum -= nums[left];
            left++;
        }
    }

    return (minLen == INT_MAX) ? 0 : minLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Minimum Window
## 🌍 Real World Use
Minimum time/length to reach threshold
Resource optimization
