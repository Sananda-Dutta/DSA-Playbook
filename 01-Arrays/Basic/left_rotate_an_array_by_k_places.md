# 🧩 Left Rotate an Array by K Places
## 🧠 Intuition

We need to rotate the array to the left by k steps.

## 👉 Key idea:

Elements shift left
First k elements move to the end
## 🐢 Brute Force Approach
Rotate one step at a time k times
```cpp
#include <vector>
using namespace std;

void leftRotate(vector<int>& nums, int k) {
    int n = nums.size();
    k = k % n;

    for (int i = 0; i < k; i++) {
        int first = nums[0];
        for (int j = 0; j < n - 1; j++) {
            nums[j] = nums[j + 1];
        }
        nums[n - 1] = first;
    }
}
```
## ⚡ Better Approach (Extra Array)
Store first k elements
Shift remaining
Append stored elements
```cpp
#include <vector>
using namespace std;

void leftRotate(vector<int>& nums, int k) {
    int n = nums.size();
    k = k % n;

    vector<int> temp;

    for (int i = 0; i < k; i++) {
        temp.push_back(nums[i]);
    }

    for (int i = k; i < n; i++) {
        nums[i - k] = nums[i];
    }

    for (int i = 0; i < temp.size(); i++) {
        nums[n - k + i] = temp[i];
    }
}
```
## 🚀 Optimal Approach (Reversal Algorithm)
Reverse in 3 steps:
Reverse first k elements
Reverse remaining
Reverse entire array
```cpp
#include <vector>
#include <algorithm>
using namespace std;

void leftRotate(vector<int>& nums, int k) {
    int n = nums.size();
    k = k % n;

    reverse(nums.begin(), nums.begin() + k);
    reverse(nums.begin() + k, nums.end());
    reverse(nums.begin(), nums.end());
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Array Rotation
Reversal Technique
## 🌍 Real World Use
Circular shifts in data
Rotating buffers / queues
