# 🧩 Shortest Subarray with Sum ≥ K (with Negatives)
## 🧠 Intuition

Array may contain negative numbers, so normal sliding window ❌

## 👉 Key idea:

Use Prefix Sum + Monotonic Deque
Maintain increasing prefix sums
Check smallest valid window
## 🐢 Brute Force Approach
Generate all subarrays
Check sum ≥ k
Track minimum length
```cpp
#include <vector>
#include <climits>
using namespace std;

int shortestSubarray(vector<int>& nums, int k) {
    int n = nums.size();
    int minLen = INT_MAX;

    for (int i = 0; i < n; i++) {
        long long sum = 0;
        for (int j = i; j < n; j++) {
            sum += nums[j];
            if (sum >= k) {
                minLen = min(minLen, j - i + 1);
                break;
            }
        }
    }

    return (minLen == INT_MAX) ? -1 : minLen;
}
```
## ⚡ Better Approach (Prefix Sum)
Still O(n²) → not optimal
## 🚀 Optimal Approach (Monotonic Deque)
### Steps:
Build prefix sum array
Use deque to store indices
Maintain increasing prefix sum
Remove invalid indices
```cpp
#include <vector>
#include <deque>
#include <climits>
using namespace std;

int shortestSubarray(vector<int>& nums, int k) {
    int n = nums.size();
    vector<long long> prefix(n + 1, 0);

    for (int i = 0; i < n; i++) {
        prefix[i + 1] = prefix[i] + nums[i];
    }

    deque<int> dq;
    int minLen = INT_MAX;

    for (int i = 0; i <= n; i++) {
        while (!dq.empty() && prefix[i] - prefix[dq.front()] >= k) {
            minLen = min(minLen, i - dq.front());
            dq.pop_front();
        }

        while (!dq.empty() && prefix[i] <= prefix[dq.back()]) {
            dq.pop_back();
        }

        dq.push_back(i);
    }

    return (minLen == INT_MAX) ? -1 : minLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)
## 🔁 Pattern
Prefix Sum
Monotonic Deque
## 🌍 Real World Use
Shortest interval reaching threshold (with fluctuations)
Financial analytics with losses/gains
