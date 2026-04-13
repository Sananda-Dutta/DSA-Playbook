# 🧩 Max Consecutive Ones III
## 🧠 Intuition

We can flip at most k zeros → find longest subarray with at most k zeros.

## 👉 Key idea:

Sliding window
Maintain count of zeros
Shrink when zeros > k
## 🐢 Brute Force Approach
Generate all subarrays
Count zeros ≤ k
```cpp
#include <vector>
using namespace std;

int longestOnes(vector<int>& nums, int k) {
    int n = nums.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int zeroCount = 0;

        for (int j = i; j < n; j++) {
            if (nums[j] == 0) zeroCount++;

            if (zeroCount <= k) {
                maxLen = max(maxLen, j - i + 1);
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
## 🚀 Optimal Approach (Sliding Window)
### Steps:
Expand window
Count zeros
If zeros > k → shrink
Track max length
```cpp
#include <vector>
using namespace std;

int longestOnes(vector<int>& nums, int k) {
    int left = 0, zeroCount = 0, maxLen = 0;

    for (int right = 0; right < nums.size(); right++) {
        if (nums[right] == 0) zeroCount++;

        while (zeroCount > k) {
            if (nums[left] == 0) zeroCount--;
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
At Most K Constraint
## 🌍 Real World Use
Error-tolerant signal processing
Longest stable segment with limited fault
