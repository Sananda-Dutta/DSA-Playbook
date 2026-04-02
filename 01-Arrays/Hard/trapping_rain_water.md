# 🧩 Trapping Rain Water
## 🧠 Intuition

Water trapped at any index depends on:
👉 min(leftMax, rightMax) - height[i]

## Key idea:

For each bar, find tallest on left & right
Water is limited by the smaller one
## 🐢 Brute Force Approach
For each index:
Find left max
Find right max
Compute trapped water
```cpp
#include <vector>
using namespace std;

int trap(vector<int>& height) {
    int n = height.size();
    int water = 0;

    for (int i = 0; i < n; i++) {
        int leftMax = 0, rightMax = 0;

        for (int j = 0; j <= i; j++) {
            leftMax = max(leftMax, height[j]);
        }

        for (int j = i; j < n; j++) {
            rightMax = max(rightMax, height[j]);
        }

        water += min(leftMax, rightMax) - height[i];
    }

    return water;
}
```
## ⚡ Better Approach (Prefix & Suffix Arrays)
Precompute:
leftMax array
rightMax array
```cpp
#include <vector>
using namespace std;

int trap(vector<int>& height) {
    int n = height.size();
    vector<int> leftMax(n), rightMax(n);

    leftMax[0] = height[0];
    for (int i = 1; i < n; i++) {
        leftMax[i] = max(leftMax[i - 1], height[i]);
    }

    rightMax[n - 1] = height[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        rightMax[i] = max(rightMax[i + 1], height[i]);
    }

    int water = 0;
    for (int i = 0; i < n; i++) {
        water += min(leftMax[i], rightMax[i]) - height[i];
    }

    return water;
}
```
## 🚀 Optimal Approach (Two Pointer)
Use two pointers:
left, right
Track leftMax, rightMax
Steps:
Move smaller side
Accumulate water
```cpp
#include <vector>
using namespace std;

int trap(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int leftMax = 0, rightMax = 0;
    int water = 0;

    while (left <= right) {
        if (height[left] <= height[right]) {
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                water += leftMax - height[left];
            }
            left++;
        } else {
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                water += rightMax - height[right];
            }
            right--;
        }
    }

    return water;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Two Pointer
Prefix/Suffix Max
## 🌍 Real World Use
Rainwater collection systems
Terrain water storage simulation
