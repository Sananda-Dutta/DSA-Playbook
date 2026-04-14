# 🧩 Subarrays with Product Less Than K
## 🧠 Intuition

We need count of subarrays where product < k.

## 👉 Key idea:

Use sliding window
Multiply while expanding
Divide while shrinking
## 🐢 Brute Force Approach
Generate all subarrays
Compute product
```cpp
#include <vector>
using namespace std;

int numSubarrayProductLessThanK(vector<int>& nums, int k) {
    int n = nums.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        long long prod = 1;

        for (int j = i; j < n; j++) {
            prod *= nums[j];
            if (prod < k) count++;
            else break;
        }
    }

    return count;
}
```
## ⚡ Better Approach (if any)
Not needed → directly optimal
## 🚀 Optimal Approach (Sliding Window)
Steps:
Expand window → multiply
If product ≥ k → shrink
Add (right - left + 1)
```cpp
#include <vector>
using namespace std;

int numSubarrayProductLessThanK(vector<int>& nums, int k) {
    if (k <= 1) return 0;

    int left = 0, count = 0;
    long long prod = 1;

    for (int right = 0; right < nums.size(); right++) {
        prod *= nums[right];

        while (prod >= k) {
            prod /= nums[left];
            left++;
        }

        count += (right - left + 1);
    }

    return count;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Multiplicative Window
## 🌍 Real World Use
Financial thresholds (product constraints)
Probability chain
