# 🧩 Set Matrix Zeroes
## 🧠 Intuition

If any cell is 0, its entire row and column must be set to 0.

## 👉 Key idea:

Use first row & column as markers to avoid extra space
## 🐢 Brute Force Approach
When a 0 is found → mark entire row & column with a special value (e.g., -1)
Later convert -1 → 0
```cpp
#include <vector>
using namespace std;

void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();

    // Mark
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix[i][j] == 0) {
                for (int k = 0; k < m; k++) {
                    if (matrix[i][k] != 0) matrix[i][k] = -1;
                }
                for (int k = 0; k < n; k++) {
                    if (matrix[k][j] != 0) matrix[k][j] = -1;
                }
            }
        }
    }

    // Convert -1 → 0
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix[i][j] == -1) matrix[i][j] = 0;
        }
    }
}
```
## ⚡ Better Approach (Extra Arrays)
Use two arrays:
row[]
col[]
```cpp
#include <vector>
using namespace std;

void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();
    vector<int> row(n, 0), col(m, 0);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix[i][j] == 0) {
                row[i] = 1;
                col[j] = 1;
            }
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (row[i] || col[j]) {
                matrix[i][j] = 0;
            }
        }
    }
}
```
## 🚀 Optimal Approach (O(1) Space)
Use first row & column as markers
Use a variable for column 0
```cpp
#include <vector>
using namespace std;

void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();
    int col0 = 1;

    for (int i = 0; i < n; i++) {
        if (matrix[i][0] == 0) col0 = 0;

        for (int j = 1; j < m; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    for (int i = n - 1; i >= 0; i--) {
        for (int j = m - 1; j >= 1; j--) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }

        if (col0 == 0) matrix[i][0] = 0;
    }
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n × m)
Space Complexity: O(1)
## 🔁 Pattern
Matrix Manipulation
In-place Marking
## 🌍 Real World Use
Image masking
Data cleaning in matrices
