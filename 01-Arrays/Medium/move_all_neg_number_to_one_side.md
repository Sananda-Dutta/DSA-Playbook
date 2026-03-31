# 🧩 Move All Negative Numbers to One Side
## 🧠 Intuition

We need to rearrange the array so that all negative numbers come to one side (order not important).

## 👉 Key idea:

Similar to partitioning
Use two pointers or partition logic
## 🐢 Brute Force Approach
Create a new array
First add negatives, then positives
```cpp
#include <vector>
using namespace std;

vector<int> moveNegatives(vector<int>& nums) {
    vector<int> result;

    for (int num : nums) {
        if (num < 0) result.push_back(num);
    }

    for (int num : nums) {
        if (num >= 0) result.push_back(num);
    }

    return result;
}
```
## ⚡ Better Approach (Partition Logic with Extra Space Avoided)
Similar to QuickSort partition
Swap negatives to front
## 🚀 Optimal Approach (Two Pointer - In-place)
Use two pointers:
left → start
right → end
Steps:
If left is negative → move forward
If right is positive → move backward
Else swap
```cpp
#include <vector>
using namespace std;

void moveNegatives(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;

    while (left <= right) {
        if (nums[left] < 0) {
            left++;
        } 
        else if (nums[right] >= 0) {
            right--;
        } 
        else {
            swap(nums[left], nums[right]);
            left++;
            right--;
        }
    }
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Two Pointer
Partition (QuickSort style)
## 🌍 Real World Use
Segregating data based on condition (e.g., valid/invalid entries)
Preprocessing before algorithms
