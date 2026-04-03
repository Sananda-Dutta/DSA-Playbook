🧩 Remove Duplicates from Sorted Array ⭐
🧠 Intuition

Since the array is sorted, duplicates are adjacent.

👉 Key idea:

Use two pointers
Place unique elements at the front
🐢 Brute Force Approach
Use a set to store unique elements
Copy back to array
Code
#include <vector>
#include <set>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    set<int> s(nums.begin(), nums.end());
    int i = 0;

    for (int x : s) {
        nums[i++] = x;
    }

    return i;
}
⚡ Better Approach (Extra Array)
Store unique elements in another array
Code
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    vector<int> temp;
    temp.push_back(nums[0]);

    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] != nums[i - 1]) {
            temp.push_back(nums[i]);
        }
    }

    for (int i = 0; i < temp.size(); i++) {
        nums[i] = temp[i];
    }

    return temp.size();
}
🚀 Optimal Approach (Two Pointer)
Use:
i → last unique index
j → traversal
Code
#include <vector>
using namespace std;

int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;

    int i = 0;

    for (int j = 1; j < nums.size(); j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }

    return i + 1;
}
⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
🔁 Pattern
Two Pointer (Slow & Fast)
🌍 Real World Use
Removing duplicates in sorted datasets
Data cleaning pipelines
