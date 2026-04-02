# 🧩 Jump Game II
## 🧠 Intuition

We need minimum number of jumps to reach last index.

## 👉 Key idea:

Use greedy + level traversal
Think like BFS on array
## 🐢 Brute Force Approach
Try all paths recursively
Track minimum jumps
```cpp
#include <vector>
#include <climits>
using namespace std;

int solve(vector<int>& nums, int index) {
    if (index >= nums.size() - 1) return 0;

    int minJumps = INT_MAX;
    int maxJump = nums[index];

    for (int step = 1; step <= maxJump; step++) {
        int jumps = solve(nums, index + step);
        if (jumps != INT_MAX) {
            minJumps = min(minJumps, 1 + jumps);
        }
    }

    return minJumps;
}

int jump(vector<int>& nums) {
    return solve(nums, 0);
}
```
## ⚡ Better Approach (DP)
Use dp array to store min jumps
```cpp
#include <vector>
#include <climits>
using namespace std;

int jump(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, INT_MAX);
    dp[0] = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 1; j <= nums[i] && i + j < n; j++) {
            dp[i + j] = min(dp[i + j], dp[i] + 1);
        }
    }

    return dp[n - 1];
}
```
## 🚀 Optimal Approach (Greedy)
### Track:
currentEnd → boundary of current jump
farthest → farthest reachable
### Steps:
Traverse array
When reach currentEnd, increase jump
```cpp
#include <vector>
using namespace std;

int jump(vector<int>& nums) {
    int jumps = 0;
    int currentEnd = 0;
    int farthest = 0;

    for (int i = 0; i < nums.size() - 1; i++) {
        farthest = max(farthest, i + nums[i]);

        if (i == currentEnd) {
            jumps++;
            currentEnd = farthest;
        }
    }

    return jumps;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Greedy
BFS-like traversal
## 🌍 Real World Use
Minimum steps in path traversal
Network routing optimization
