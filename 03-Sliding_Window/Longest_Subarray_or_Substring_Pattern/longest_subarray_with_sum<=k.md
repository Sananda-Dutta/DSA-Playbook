# 🧩 Longest Subarray with Sum ≤ K
## 🧠 Intuition

We need the longest subarray whose sum is ≤ k.

## 👉 Key idea:

Use sliding window (only works when all numbers are non-negative)
Expand window while sum ≤ k
Shrink when sum > k
## 🐢 Brute Force Approach
Generate all subarrays
Check sum ≤ k
```cpp
#include <vector>
using namespace std;

int longestSubarray(vector<int>& nums, int k) {
    int n = nums.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum <= k) {
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (if any)
For negative numbers → need prefix sum + binary search (advanced)
🚀 Optimal Approach (Sliding Window - Non-negative only)
### Steps:
Expand window → add nums[right]
If sum > k → shrink from left
Track max length
```cpp
#include <vector>
using namespace std;

int longestSubarray(vector<int>& nums, int k) {
    int left = 0, sum = 0, maxLen = 0;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];

        while (sum > k) {
            sum -= nums[left];
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Longest Subarray with Condition
## 🌍 Real World Use
Budget-constrained segments
Longest valid time window under limit
