# 🧩 Sliding Window Maximum
## 🧠 Intuition

We need the maximum element in every window of size k.

## 👉 Key idea:

Maintain a deque (double-ended queue)
Store indices of useful elements
Ensure:
Elements are in decreasing order
Front always holds max
## 🐢 Brute Force Approach
For every window:
Traverse k elements
Find max
```cpp
#include <vector>
using namespace std;

vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;

    for (int i = 0; i <= nums.size() - k; i++) {
        int maxi = nums[i];
        for (int j = i; j < i + k; j++) {
            maxi = max(maxi, nums[j]);
        }
        result.push_back(maxi);
    }

    return result;
}
```
## ⚡ Better Approach (Heap / Priority Queue)
Use max heap
Push elements with indices
Remove outdated elements
```cpp
#include <vector>
#include <queue>
using namespace std;

vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    priority_queue<pair<int,int>> pq;

    for (int i = 0; i < nums.size(); i++) {
        pq.push({nums[i], i});

        while (pq.top().second <= i - k) {
            pq.pop();
        }

        if (i >= k - 1) {
            result.push_back(pq.top().first);
        }
    }

    return result;
}
```
## 🚀 Optimal Approach (Deque)
Use deque to store indices
Maintain decreasing order
### Steps:
Remove elements out of window
Remove smaller elements from back
Add current index
Front = max
```cpp
#include <vector>
#include <deque>
using namespace std;

vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> result;

    for (int i = 0; i < nums.size(); i++) {
        // Remove out of window
        if (!dq.empty() && dq.front() == i - k) {
            dq.pop_front();
        }

        // Remove smaller elements
        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }

        dq.push_back(i);

        if (i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }

    return result;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(k)
## 🔁 Pattern
Sliding Window
Monotonic Deque
## 🌍 Real World Use
Real-time analytics (max in last k seconds)
Stock price windows
Stream processing
