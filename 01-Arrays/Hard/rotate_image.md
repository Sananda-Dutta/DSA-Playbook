# 🧩 Rotate Image (90° Clockwise)
## 🧠 Intuition

We need to rotate an n x n matrix by 90° clockwise in-place.

## 👉 Key idea:

Rotation = Transpose + Reverse each row
## 🐢 Brute Force Approach
Create a new matrix
Place elements at rotated positions
```cpp
#include <vector>
using namespace std;

void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size();
    vector<vector<int>> temp(n, vector<int>(n));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            temp[j][n - 1 - i] = matrix[i][j];
        }
    }

    matrix = temp;
}
```
## ⚡ Better Approach (if any)
Direct rotation layer by layer (more complex)
## 🚀 Optimal Approach (Transpose + Reverse)
Step 1: Transpose matrix
Step 2: Reverse each row
```cpp
#include <vector>
#include <algorithm>
using namespace std;

void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size();

    // Transpose
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }

    // Reverse each row
    for (int i = 0; i < n; i++) {
        reverse(matrix[i].begin(), matrix[i].end());
    }
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n²)
Space Complexity: O(1)
## 🔁 Pattern
Matrix Manipulation
Transpose + Reverse
## 🌍 Real World Use
Image processing (rotation)
Graphics transformations
