# 🧩 1. Two Sum
##🧠 Intuition
We need to find two numbers whose sum = target.
Brute force checks all pairs, but that’s slow.
Better thinking:
👉 “Can I remember what I’ve seen before?” → use a HashMap

## 🐢 Brute Force Approach
Check every pair (i, j)
If sum equals target → return indices
Code (Python)
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    int n = nums.size();
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (nums[i] + nums[j] == target) {
                return {i, j};
            }
        }
    }
    return {};
}
```
## ⚡ Better Approach (if any)
Sort + Two Pointer
❌ Not ideal because we lose original indices

##🚀 Optimal Approach
Use a HashMap (value → index)
For each element:
Compute complement = target - num
If complement exists → return indices
Else store current element
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> mp;

    for (int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];

        if (mp.find(complement) != mp.end()) {
            return {mp[complement], i};
        }

        mp[nums[i]] = i;
    }

    return {};
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)

## 🔁 Pattern

👉 HashMap + Lookup

## 🌍 Real World Use
Finding pairs of transactions matching a budget
Matching complementary data values in databases
## 🎨 Visualization
