# 🧩 Spiral Matrix
## 🧠 Intuition

We need to traverse matrix in spiral order.

## 👉 Key idea:

Maintain 4 boundaries:
top, bottom, left, right
Traverse layer by layer
## 🐢 Brute Force Approach
Mark visited cells and simulate spiral
## ⚡ Better Approach (Boundary Traversal)
Use boundaries instead of visited array
## 🚀 Optimal Approach
### Steps:
Traverse left → right
top++
Traverse top → bottom
right--
Traverse right → left
bottom--
Traverse bottom → top
left++
```cpp
#include <vector>
using namespace std;

vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;

    int top = 0, bottom = matrix.size() - 1;
    int left = 0, right = matrix[0].size() - 1;

    while (top <= bottom && left <= right) {
        // left -> right
        for (int i = left; i <= right; i++) {
            result.push_back(matrix[top][i]);
        }
        top++;

        // top -> bottom
        for (int i = top; i <= bottom; i++) {
            result.push_back(matrix[i][right]);
        }
        right--;

        if (top <= bottom) {
            // right -> left
            for (int i = right; i >= left; i--) {
                result.push_back(matrix[bottom][i]);
            }
            bottom--;
        }

        if (left <= right) {
            // bottom -> top
            for (int i = bottom; i >= top; i--) {
                result.push_back(matrix[i][left]);
            }
            left++;
        }
    }

    return result;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n × m)
Space Complexity: O(1) (excluding output)
## 🔁 Pattern
Matrix Traversal
Boundary Control
## 🌍 Real World Use
Image scanning
Layer-by-layer data processing
