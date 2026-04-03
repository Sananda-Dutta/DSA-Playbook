# 🧩 Equilibrium Index
## 🧠 Intuition

An equilibrium index is where:
👉 sum of left elements == sum of right elements

## Key idea:

Compute total sum
Traverse and maintain left sum
Right sum = total - left - current
## 🐢 Brute Force Approach
For each index:
Compute left sum
Compute right sum
Compare
```cpp
#include <vector>
using namespace std;

int equilibriumIndex(vector<int>& nums) {
    int n = nums.size();

    for (int i = 0; i < n; i++) {
        int leftSum = 0, rightSum = 0;

        for (int j = 0; j < i; j++) leftSum += nums[j];
        for (int j = i + 1; j < n; j++) rightSum += nums[j];

        if (leftSum == rightSum) return i;
    }

    return -1;
}
```
## ⚡ Better Approach (Prefix Sum Array)
Precompute prefix sums
Use them to get left & right sums
```cpp
#include <vector>
using namespace std;

int equilibriumIndex(vector<int>& nums) {
    int n = nums.size();
    vector<int> prefix(n);

    prefix[0] = nums[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + nums[i];
    }

    for (int i = 0; i < n; i++) {
        int leftSum = (i == 0) ? 0 : prefix[i - 1];
        int rightSum = prefix[n - 1] - prefix[i];

        if (leftSum == rightSum) return i;
    }

    return -1;
}
```
## 🚀 Optimal Approach
Use running sums (no extra space)
```cpp
#include <vector>
using namespace std;

int equilibriumIndex(vector<int>& nums) {
    int total = 0;
    for (int num : nums) total += num;

    int leftSum = 0;

    for (int i = 0; i < nums.size(); i++) {
        int rightSum = total - leftSum - nums[i];

        if (leftSum == rightSum) return i;

        leftSum += nums[i];
    }

    return -1;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Prefix Sum
Running Sum
## 🌍 Real World Use
Balance point detection in datasets
Load balancing / partitioning
