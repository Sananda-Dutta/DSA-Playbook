# 🧩 Binary Subarrays With Sum
## 🧠 Intuition

We need to count subarrays with sum = goal in a binary array.

## 👉 Key idea:

Use prefix sum + hashmap

OR use sliding window trick:

count(sum == goal) = count(sum ≤ goal) - count(sum ≤ goal-1)
## 🐢 Brute Force Approach
Generate all subarrays
Count those with sum = goal
```cpp
#include <vector>
using namespace std;

int numSubarraysWithSum(vector<int>& nums, int goal) {
    int n = nums.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum == goal) count++;
        }
    }

    return count;
}
```
## ⚡ Better Approach (Prefix Sum + HashMap)
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int numSubarraysWithSum(vector<int>& nums, int goal) {
    unordered_map<int, int> mp;
    mp[0] = 1;

    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;

        if (mp.find(sum - goal) != mp.end()) {
            count += mp[sum - goal];
        }

        mp[sum]++;
    }

    return count;
}
```
## 🚀 Optimal Approach (Sliding Window Trick)
Helper:
Count subarrays with sum ≤ k
```cpp
#include <vector>
using namespace std;

int atMost(vector<int>& nums, int goal) {
    if (goal < 0) return 0;

    int left = 0, sum = 0, count = 0;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];

        while (sum > goal) {
            sum -= nums[left];
            left++;
        }

        count += (right - left + 1);
    }

    return count;
}

int numSubarraysWithSum(vector<int>& nums, int goal) {
    return atMost(nums, goal) - atMost(nums, goal - 1);
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Prefix Sum
## 🌍 Real World Use
Counting exact target events in binary streams
Signal processing
