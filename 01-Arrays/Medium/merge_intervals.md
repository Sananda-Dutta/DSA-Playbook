# 🧩 Merge Intervals
## 🧠 Intuition

We are given intervals → need to merge overlapping ones.

## 👉 Key idea:

Sort intervals by start time
Merge when overlapping
## 🐢 Brute Force Approach
Compare every pair of intervals
Merge overlapping ones repeatedly
```cpp
#include <vector>
using namespace std;

vector<vector<int>> merge(vector<vector<int>>& intervals) {
    int n = intervals.size();
    vector<bool> merged(n, false);
    vector<vector<int>> result;

    for (int i = 0; i < n; i++) {
        if (merged[i]) continue;

        int start = intervals[i][0];
        int end = intervals[i][1];

        for (int j = i + 1; j < n; j++) {
            if (!merged[j] && !(intervals[j][0] > end || intervals[j][1] < start)) {
                start = min(start, intervals[j][0]);
                end = max(end, intervals[j][1]);
                merged[j] = true;
            }
        }

        result.push_back({start, end});
    }

    return result;
}
```
## ⚡ Better Approach (if any)
Sorting helps reduce comparisons
## 🚀 Optimal Approach
Sort intervals based on start
Traverse and merge
### Steps:
If current interval overlaps → merge
Else → push previous and move ahead
```cpp
#include <vector>
#include <algorithm>
using namespace std;

vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> result;

    sort(intervals.begin(), intervals.end());

    for (auto& interval : intervals) {
        if (result.empty() || result.back()[1] < interval[0]) {
            result.push_back(interval);
        } else {
            result.back()[1] = max(result.back()[1], interval[1]);
        }
    }

    return result;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n log n) (sorting)
Space Complexity: O(n)
## 🔁 Pattern
Interval Merging
Sorting + Greedy
## 🌍 Real World Use
Calendar scheduling (merge meeting times)
Booking systems (merge occupied slots)
Resource allocation timelines