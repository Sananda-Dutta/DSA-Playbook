# 🧩 Count Subarrays with Given Sum (K)
## 🧠 Intuition

We need to count the number of subarrays whose sum equals k.

## 👉 Key idea:

Use prefix sum
If currentSum - k exists before → a valid subarray exists
## 🐢 Brute Force Approach
Generate all subarrays
Count those with sum = k
```cpp
#include <vector>
using namespace std;

int subarraySum(vector<int>& nums, int k) {
    int n = nums.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum == k) {
                count++;
            }
        }
    }

    return count;
}
```
## ⚡ Better Approach (if any)
No major improvement beyond this → go optimal
## 🚀 Optimal Approach (Prefix Sum + HashMap)
### Maintain:
sum → running prefix sum
map → frequency of prefix sums
### Steps:
For each element:
Add to sum
Check if (sum - k) exists → add its frequency
Store current sum in map
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    mp[0] = 1; // base case

    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;

        if (mp.find(sum - k) != mp.end()) {
            count += mp[sum - k];
        }

        mp[sum]++;
    }

    return count;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)
## 🔁 Pattern
Prefix Sum
HashMap
## 🌍 Real World Use
Counting patterns in financial transactions
Detecting number of intervals with fixed total
Analytics on time-series data
