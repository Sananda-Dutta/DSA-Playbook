# 🧩 Median of Two Sorted Arrays
## 🧠 Intuition

We need median of two sorted arrays without merging fully.

## 👉 Key idea:

Use Binary Search on smaller array
Partition arrays such that:
Left half ≤ Right half
## 🐢 Brute Force Approach
Merge arrays
Sort
Find median
```cpp
#include <vector>
#include <algorithm>
using namespace std;

double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    vector<int> merged = nums1;
    merged.insert(merged.end(), nums2.begin(), nums2.end());

    sort(merged.begin(), merged.end());

    int n = merged.size();
    if (n % 2 == 0) {
        return (merged[n/2 - 1] + merged[n/2]) / 2.0;
    } else {
        return merged[n/2];
    }
}
```
## ⚡ Better Approach (Merge without extra sorting)
Use two pointers to merge partially
```cpp
#include <vector>
using namespace std;

double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    vector<int> merged;
    int i = 0, j = 0;

    while (i < nums1.size() && j < nums2.size()) {
        if (nums1[i] < nums2[j]) merged.push_back(nums1[i++]);
        else merged.push_back(nums2[j++]);
    }

    while (i < nums1.size()) merged.push_back(nums1[i++]);
    while (j < nums2.size()) merged.push_back(nums2[j++]);

    int n = merged.size();
    if (n % 2 == 0) {
        return (merged[n/2 - 1] + merged[n/2]) / 2.0;
    } else {
        return merged[n/2];
    }
}
```
## 🚀 Optimal Approach (Binary Search)
Always binary search on smaller array
Key Conditions:
Partition arrays so:
maxLeft1 <= minRight2
maxLeft2 <= minRight1
```cpp
#include <vector>
#include <climits>
using namespace std;

double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    if (nums1.size() > nums2.size()) {
        return findMedianSortedArrays(nums2, nums1);
    }

    int n1 = nums1.size(), n2 = nums2.size();
    int low = 0, high = n1;

    while (low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = (n1 + n2 + 1) / 2 - cut1;

        int left1 = (cut1 == 0) ? INT_MIN : nums1[cut1 - 1];
        int left2 = (cut2 == 0) ? INT_MIN : nums2[cut2 - 1];

        int right1 = (cut1 == n1) ? INT_MAX : nums1[cut1];
        int right2 = (cut2 == n2) ? INT_MAX : nums2[cut2];

        if (left1 <= right2 && left2 <= right1) {
            if ((n1 + n2) % 2 == 0) {
                return (max(left1, left2) + min(right1, right2)) / 2.0;
            } else {
                return max(left1, left2);
            }
        } 
        else if (left1 > right2) {
            high = cut1 - 1;
        } 
        else {
            low = cut1 + 1;
        }
    }

    return 0.0;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(log(min(n, m)))
Space Complexity: O(1)
## 🔁 Pattern
Binary Search on Answer
Partitioning
## 🌍 Real World Use
Median in streaming/merged datasets
Load balancing & statistics
