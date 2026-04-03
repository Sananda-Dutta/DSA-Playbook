# 🧩 Non-Overlapping Intervals
## 🧠 Intuition

We need to remove minimum intervals so that no intervals overlap.

👉 Equivalent to:

Select maximum non-overlapping intervals
Greedy based on earliest ending time
## 🐢 Brute Force Approach
Try all subsets
Check for overlap
Track minimum removals
```cpp
#include <vector>
using namespace std;

bool isOverlap(vector<int>& a, vector<int>& b) {
    return !(a[1] <= b[0] || b[1] <= a[0]);
}
```
// Not practical brute (exponential), shown conceptually
## ⚡ Better Approach (Sorting by Start)
Sort intervals
Compare adjacent
## 🚀 Optimal Approach (Greedy)
Sort by end time
Keep track of last selected interval
If overlap → remove one
```cpp
#include <vector>
#include <algorithm>
using namespace std;

int eraseOverlapIntervals(vector<vector<int>>& intervals) {
    if (intervals.empty()) return 0;

    sort(intervals.begin(), intervals.end(), [](auto& a, auto& b) {
        return a[1] < b[1];
    });

    int count = 0;
    int end = intervals[0][1];

    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i][0] < end) {
            count++; // remove this interval
        } else {
            end = intervals[i][1];
        }
    }

    return count;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n log n)
Space Complexity: O(1)
## 🔁 Pattern
Greedy
Interval Scheduling
## 🌍 Real World Use
Meeting room scheduling
Task planning without conflicts
Resource allocation systems
