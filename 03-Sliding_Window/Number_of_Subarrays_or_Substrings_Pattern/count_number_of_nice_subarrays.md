# 🧩 Count Number of Nice Subarrays
## 🧠 Intuition

We need subarrays with exactly k odd numbers.

## 👉 Key idea:

Convert problem:
odd → 1
even → 0
Then it becomes Binary Subarray Sum = k

OR directly use sliding window trick

## 🐢 Brute Force Approach
Generate all subarrays
Count odd numbers
```cpp
#include <vector>
using namespace std;

int numberOfSubarrays(vector<int>& nums, int k) {
    int n = nums.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        int odd = 0;

        for (int j = i; j < n; j++) {
            if (nums[j] % 2) odd++;

            if (odd == k) count++;
        }
    }

    return count;
}
```
## ⚡ Better Approach (Prefix Sum)
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int numberOfSubarrays(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    mp[0] = 1;

    int odd = 0, count = 0;

    for (int num : nums) {
        if (num % 2) odd++;

        if (mp.find(odd - k) != mp.end()) {
            count += mp[odd - k];
        }

        mp[odd]++;
    }

    return count;
}
```
## 🚀 Optimal Approach (Sliding Window Trick)
Idea:
exactly(k) = atMost(k) - atMost(k-1)
```cpp
#include <vector>
using namespace std;

int atMost(vector<int>& nums, int k) {
    int left = 0, count = 0, odd = 0;

    for (int right = 0; right < nums.size(); right++) {
        if (nums[right] % 2) odd++;

        while (odd > k) {
            if (nums[left] % 2) odd--;
            left++;
        }

        count += (right - left + 1);
    }

    return count;
}

int numberOfSubarrays(vector<int>& nums, int k) {
    return atMost(nums, k) - atMost(nums, k - 1);
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Exactly K = AtMost(K) - AtMost(K-1)
## 🌍 Real World Use
Counting segments with exact constraint
Pattern detection in streams
