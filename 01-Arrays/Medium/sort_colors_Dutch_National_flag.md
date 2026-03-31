# 🧩 Sort Colors (Dutch National Flag)
## 🧠 Intuition

We are given an array with only 0, 1, 2.
👉 Goal: sort in-place without using extra space or sort function

## Key idea:

Divide array into 3 parts:
0s → left
1s → middle
2s → right
# 🐢 Brute Force Approach
Use sorting algorithm (sort())
```cpp
#include <vector>
#include <algorithm>
using namespace std;

void sortColors(vector<int>& nums) {
    sort(nums.begin(), nums.end());
}
```
# ⚡ Better Approach (Counting Sort)
Count number of 0s, 1s, 2s
Overwrite array
```cpp
#include <vector>
using namespace std;

void sortColors(vector<int>& nums) {
    int count0 = 0, count1 = 0, count2 = 0;

    for (int num : nums) {
        if (num == 0) count0++;
        else if (num == 1) count1++;
        else count2++;
    }

    int i = 0;
    while (count0--) nums[i++] = 0;
    while (count1--) nums[i++] = 1;
    while (count2--) nums[i++] = 2;
}
```
# 🚀 Optimal Approach (Dutch National Flag Algorithm)
Use 3 pointers:
low → next position for 0
mid → current element
high → next position for 2
Steps:
If nums[mid] == 0 → swap with low, move both
If nums[mid] == 1 → move mid
If nums[mid] == 2 → swap with high, move high
```cpp
#include <vector>
using namespace std;

void sortColors(vector<int>& nums) {
    int low = 0, mid = 0, high = nums.size() - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++;
            mid++;
        } 
        else if (nums[mid] == 1) {
            mid++;
        } 
        else {
            swap(nums[mid], nums[high]);
            high--;
        }
    }
}
```
# ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
# 🔁 Pattern
Three Pointer
Dutch National Flag
# 🌍 Real World Use
Partitioning problems
Categorizing data into fixed groups efficiently
