# 🧩 Gas Station
## 🧠 Intuition

We need to find a starting index such that we can complete the circuit.

## 👉 Key idea:

If total gas < total cost → impossible
Otherwise:
Reset start whenever tank becomes negative
## 🐢 Brute Force Approach
Try each index as start
Simulate full cycle
```cpp
#include <vector>
using namespace std;

int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int n = gas.size();

    for (int start = 0; start < n; start++) {
        int tank = 0;
        bool possible = true;

        for (int i = 0; i < n; i++) {
            int idx = (start + i) % n;
            tank += gas[idx] - cost[idx];

            if (tank < 0) {
                possible = false;
                break;
            }
        }

        if (possible) return start;
    }

    return -1;
}
```
## ⚡ Better Approach (if any)
Observation-based → go optimal
## 🚀 Optimal Approach (Greedy)
### Maintain:
total → overall gas balance
tank → current fuel
start → candidate index
### Steps:
Traverse once
If tank < 0 → reset start
```cpp
#include <vector>
using namespace std;

int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int total = 0, tank = 0, start = 0;

    for (int i = 0; i < gas.size(); i++) {
        int diff = gas[i] - cost[i];
        total += diff;
        tank += diff;

        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }

    return (total >= 0) ? start : -1;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Greedy
Circular Array
## 🌍 Real World Use
Route optimization (fuel/logistics)
Circular resource planning
