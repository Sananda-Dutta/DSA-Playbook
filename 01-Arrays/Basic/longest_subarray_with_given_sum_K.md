# 🧩 Longest Subarray with Sum K
## 🧠 Intuition

We need the longest subarray whose sum = K.

## 👉 Key idea:

Use prefix sum
If (currentSum - K) exists before → subarray found
## 🐢 Brute Force Approach
Generate all subarrays
Check sum
Track max length
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
            if (sum == k) {
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (Sliding Window - only for positives)
Works only if all elements are non-negative
```cpp
#include <vector>
using namespace std;

int longestSubarray(vector<int>& nums, int k) {
    int left = 0, sum = 0, maxLen = 0;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];

        while (sum > k) {
            sum -= nums[left++];
        }

        if (sum == k) {
            maxLen = max(maxLen, right - left + 1);
        }
    }

    return maxLen;
}
```
## 🚀 Optimal Approach (Prefix Sum + HashMap)
Works for negative + positive numbers
Store first occurrence of prefix sum
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int longestSubarray(vector<int>& nums, int k) {
    unordered_map<long long, int> mp;
    long long sum = 0;
    int maxLen = 0;

    for (int i = 0; i < nums.size(); i++) {
        sum += nums[i];

        if (sum == k) {
            maxLen = i + 1;
        }

        if (mp.find(sum - k) != mp.end()) {
            maxLen = max(maxLen, i - mp[sum - k]);
        }

        if (mp.find(sum) == mp.end()) {
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
Prefix Sum + HashMap
Sliding Window (special case)
## 🌍 Real World Use
Finding longest duration with fixed resource usage
Financial tracking (longest period with target balance change)
