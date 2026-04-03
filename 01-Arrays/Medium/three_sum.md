# 🧩 3 Sum
## 🧠 Intuition

We need all unique triplets such that:
👉 nums[i] + nums[j] + nums[k] = 0

## Key idea:

Sort array
Fix one element
Use two-pointer for remaining
## 🐢 Brute Force Approach
Check all triplets (i, j, k)
Avoid duplicates
```cpp
#include <vector>
using namespace std;

vector<vector<int>> threeSum(vector<int>& nums) {
    int n = nums.size();
    vector<vector<int>> res;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                if (nums[i] + nums[j] + nums[k] == 0) {
                    res.push_back({nums[i], nums[j], nums[k]});
                }
            }
        }
    }

    return res;
}
```
## ⚡ Better Approach (Hashing)
Fix one element
Use set for 2-sum
## 🚀 Optimal Approach (Sorting + Two Pointer)
Sort array
Fix i
Use left & right
### Steps:
Skip duplicates
Adjust pointers based on sum
```cpp
#include <vector>
#include <algorithm>
using namespace std;

vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    sort(nums.begin(), nums.end());

    for (int i = 0; i < nums.size(); i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;

        int left = i + 1, right = nums.size() - 1;

        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];

            if (sum < 0) {
                left++;
            } 
            else if (sum > 0) {
                right--;
            } 
            else {
                res.push_back({nums[i], nums[left], nums[right]});

                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;

                left++;
                right--;
            }
        }
    }

    return res;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n²)
Space Complexity: O(1) (excluding result)
## 🔁 Pattern
Two Pointer
Sorting
2-Sum Extension
## 🌍 Real World Use
Finding combinations matching constraints
Financial triplet balancing problems
