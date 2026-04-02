# 🧩 Jump Game
## 🧠 Intuition

Each element represents the maximum jump length from that position.
👉 We need to check if we can reach the last index

## Key idea:

Track the farthest reachable index
If at any point index > reachable → not possible
## 🐢 Brute Force Approach
Try all possible jumps using recursion
```cpp
#include <vector>
using namespace std;

bool canJumpFrom(vector<int>& nums, int index) {
    if (index >= nums.size() - 1) return true;

    int maxJump = nums[index];

    for (int step = 1; step <= maxJump; step++) {
        if (canJumpFrom(nums, index + step)) {
            return true;
        }
    }

    return false;
}

bool canJump(vector<int>& nums) {
    return canJumpFrom(nums, 0);
}
```
## ⚡ Better Approach (DP - Memoization)
Store results of visited indices
```cpp
#include <vector>
using namespace std;

bool solve(vector<int>& nums, int index, vector<int>& dp) {
    if (index >= nums.size() - 1) return true;
    if (dp[index] != -1) return dp[index];

    int maxJump = nums[index];

    for (int step = 1; step <= maxJump; step++) {
        if (solve(nums, index + step, dp)) {
            return dp[index] = 1;
        }
    }

    return dp[index] = 0;
}

bool canJump(vector<int>& nums) {
    vector<int> dp(nums.size(), -1);
    return solve(nums, 0, dp);
}
```
## 🚀 Optimal Approach (Greedy)
Track maxReach
If current index ≤ maxReach → update reach
```cpp
#include <vector>
using namespace std;

bool canJump(vector<int>& nums) {
    int maxReach = 0;

    for (int i = 0; i < nums.size(); i++) {
        if (i > maxReach) return false;

        maxReach = max(maxReach, i + nums[i]);
    }

    return true;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Greedy
Reachability
## 🌍 Real World Use
Path feasibility problems
Network reachability / routing
