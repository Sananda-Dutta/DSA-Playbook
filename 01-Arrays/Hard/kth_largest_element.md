# 🧩 Kth Largest Element in an Array
## 🧠 Intuition

We need the kth largest element (not kth distinct).

## 👉 Key idea:

Instead of sorting fully, we can:
Use a min-heap of size k
Keep only k largest elements
## 🐢 Brute Force Approach
Sort the array in descending order
Return k-1 index
```cpp
#include <vector>
#include <algorithm>
using namespace std;

int findKthLargest(vector<int>& nums, int k) {
    sort(nums.begin(), nums.end(), greater<int>());
    return nums[k - 1];
}
```
## ⚡ Better Approach (Min Heap)
Maintain a min heap of size k
Remove smallest when size exceeds k
```cpp
#include <vector>
#include <queue>
using namespace std;

int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> pq;

    for (int num : nums) {
        pq.push(num);
        if (pq.size() > k) {
            pq.pop();
        }
    }

    return pq.top();
}
```
## 🚀 Optimal Approach (QuickSelect)
Based on QuickSort partition
Average O(n)
```cpp
#include <vector>
using namespace std;

int partition(vector<int>& nums, int low, int high) {
    int pivot = nums[high];
    int i = low;

    for (int j = low; j < high; j++) {
        if (nums[j] <= pivot) {
            swap(nums[i], nums[j]);
            i++;
        }
    }
    swap(nums[i], nums[high]);
    return i;
}

int quickSelect(vector<int>& nums, int low, int high, int k) {
    int pi = partition(nums, low, high);

    if (pi == k) return nums[pi];
    else if (pi < k) return quickSelect(nums, pi + 1, high, k);
    else return quickSelect(nums, low, pi - 1, k);
}

int findKthLargest(vector<int>& nums, int k) {
    int n = nums.size();
    return quickSelect(nums, 0, n - 1, n - k);
}
```
## ⏱ Complexity Analysis
Time Complexity:
Brute: O(n log n)
Heap: O(n log k)
QuickSelect: O(n) average
Space Complexity: O(k) (heap)
## 🔁 Pattern
Heap (Priority Queue)
QuickSelect (Divide & Conquer)
## 🌍 Real World Use
Finding top-k elements (leaderboards, rankings)
Data stream processing
