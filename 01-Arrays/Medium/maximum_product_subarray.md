# 🧩 Maximum Product Subarray
## 🧠 Intuition

We need the maximum product of a contiguous subarray.

## 👉 Key challenge:

Negative numbers can turn small product → large
So we must track:
maxProduct (current max)
minProduct (current min, because negative × negative = positive)
## 🐢 Brute Force Approach
Generate all subarrays
Compute product
Track maximum
```cpp
#include <vector>
#include <climits>
using namespace std;

int maxProduct(vector<int>& nums) {
    int n = nums.size();
    int maxProd = INT_MIN;

    for (int i = 0; i < n; i++) {
        int prod = 1;
        for (int j = i; j < n; j++) {
            prod *= nums[j];
            maxProd = max(maxProd, prod);
        }
    }

    return maxProd;
}
```

## ⚡ Better Approach (if any)
Not efficient enough → go optimal
## 🚀 Optimal Approach
Maintain:
currMax → maximum product ending here
currMin → minimum product ending here
### Steps:
Traverse array
If element is negative → swap currMax and currMin
Update both values
Track global max
```cpp
#include <vector>
using namespace std;

int maxProduct(vector<int>& nums) {
    int currMax = nums[0];
    int currMin = nums[0];
    int result = nums[0];

    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] < 0) {
            swap(currMax, currMin);
        }

        currMax = max(nums[i], currMax * nums[i]);
        currMin = min(nums[i], currMin * nums[i]);

        result = max(result, currMax);
    }

    return result;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Dynamic Programming
Greedy (tracking min & max)
## 🌍 Real World Use
Financial growth analysis with losses/profits
Signal processing (max multiplicative gain segment)