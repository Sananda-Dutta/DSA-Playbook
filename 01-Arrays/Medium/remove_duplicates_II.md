
# 🧩 Remove Duplicates from Sorted Array II
## 🧠 Intuition

Array is sorted.
👉 Each element can appear at most twice

## Key idea:

Allow duplicates but only up to 2 times
Use two pointers to overwrite extra duplicates
## 🐢 Brute Force Approach
Use extra array
Add elements only if count ≤ 2
```cpp
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    vector<int> temp;

    for (int i = 0; i < nums.size(); i++) {
        if (temp.size() < 2 || nums[i] != temp[temp.size() - 2]) {
            temp.push_back(nums[i]);
        }
    }

    for (int i = 0; i < temp.size(); i++) {
        nums[i] = temp[i];
    }

    return temp.size();
}
```
## ⚡ Better Approach (if any)
Not needed — go optimal
## 🚀 Optimal Approach
Use two pointers:
i → position to place next valid element
Traverse array
Key condition:
Allow element if:
i < 2 OR
nums[j] != nums[i - 2]
```cpp
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    int i = 0;

    for (int j = 0; j < nums.size(); j++) {
        if (i < 2 || nums[j] != nums[i - 2]) {
            nums[i] = nums[j];
            i++;
        }
    }

    return i;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Two Pointer
In-place array modification
## 🌍 Real World Use
Limiting duplicate entries in logs/databases
Data compression with constraints