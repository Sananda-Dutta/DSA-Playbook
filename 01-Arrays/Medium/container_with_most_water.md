# 🧩 Container With Most Water
## 🧠 Intuition

We need to find two lines that form a container holding maximum water.

👉 Water stored = min(height[i], height[j]) * (j - i)

# Key idea:

Use two pointers
Move the pointer with smaller height (because it limits water)
# 🐢 Brute Force Approach
Check all pairs (i, j)
Calculate area
Track maximum
```cpp
#include <vector>
using namespace std;

int maxArea(vector<int>& height) {
    int n = height.size();
    int maxWater = 0;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int h = min(height[i], height[j]);
            int w = j - i;
            maxWater = max(maxWater, h * w);
        }
    }

    return maxWater;
}
```
# ⚡ Better Approach (if any)
Not required — jump to optimal
🚀 Optimal Approach (Two Pointer)
Initialize:
left = 0, right = n - 1
At each step:
Calculate area
Move pointer with smaller height
```cpp
#include <vector>
using namespace std;

int maxArea(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int maxWater = 0;

    while (left < right) {
        int h = min(height[left], height[right]);
        int w = right - left;
        maxWater = max(maxWater, h * w);

        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }

    return maxWater;
}
```
# ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
# 🔁 Pattern
Two Pointer
Greedy
# 🌍 Real World Use
Optimizing storage between boundaries
Finding maximum capacity between constraints
