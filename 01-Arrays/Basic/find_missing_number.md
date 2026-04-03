# 🧩 Find Missing Number (1 to N)
## 🧠 Intuition

We are given numbers from 1 to N with one missing.

## 👉 Key idea:

Use math or bit manipulation
## 🐢 Brute Force Approach
For each number from 1 to N, check if present
```cpp
#include <vector>
using namespace std;

int findMissing(vector<int>& nums, int n) {
    for (int i = 1; i <= n; i++) {
        bool found = false;
        for (int num : nums) {
            if (num == i) {
                found = true;
                break;
            }
        }
        if (!found) return i;
    }
    return -1;
}
```
## ⚡ Better Approach (Hashing)
Use array or set to mark presence
```cpp
#include <vector>
using namespace std;

int findMissing(vector<int>& nums, int n) {
    vector<int> hash(n + 1, 0);

    for (int num : nums) {
        hash[num] = 1;
    }

    for (int i = 1; i <= n; i++) {
        if (hash[i] == 0) return i;
    }

    return -1;
}
```
## 🚀 Optimal Approach 1 (Sum Formula)
Expected sum = n*(n+1)/2
Subtract actual sum
```cpp
#include <vector>
using namespace std;

int findMissing(vector<int>& nums, int n) {
    long long sum = 0;
    for (int num : nums) sum += num;

    long long expected = (long long)n * (n + 1) / 2;

    return expected - sum;
}
```
## 🚀 Optimal Approach 2 (XOR)
XOR all numbers from 1 to N
XOR with array elements
```cpp
#include <vector>
using namespace std;

int findMissing(vector<int>& nums, int n) {
    int xor1 = 0, xor2 = 0;

    for (int i = 1; i <= n; i++) xor1 ^= i;
    for (int num : nums) xor2 ^= num;

    return xor1 ^ xor2;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Math (Sum Formula)
Bit Manipulation (XOR)
## 🌍 Real World Use
Detect missing IDs in databases
Identify gaps in sequences
