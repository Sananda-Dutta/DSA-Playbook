# 🧩 Word Search
## 🧠 Intuition

We need to check if a word exists in the grid by moving horizontally or vertically.

## 👉 Key idea:

Use DFS + Backtracking
Mark visited cells temporarily
## 🐢 Brute Force Approach
Try all paths (inefficient without pruning)
## ⚡ Better Approach (DFS)
Start DFS from each cell
Match characters
## 🚀 Optimal Approach (Backtracking)
### Steps:
If character matches:
Mark visited
Explore 4 directions
Backtrack
```cpp
#include <vector>
#include <string>
using namespace std;

bool dfs(vector<vector<char>>& board, string& word, int i, int j, int index) {
    if (index == word.size()) return true;

    int n = board.size(), m = board[0].size();

    if (i < 0 || j < 0 || i >= n || j >= m || board[i][j] != word[index]) {
        return false;
    }

    char temp = board[i][j];
    board[i][j] = '#'; // mark visited

    bool found = dfs(board, word, i + 1, j, index + 1) ||
                 dfs(board, word, i - 1, j, index + 1) ||
                 dfs(board, word, i, j + 1, index + 1) ||
                 dfs(board, word, i, j - 1, index + 1);

    board[i][j] = temp; // backtrack

    return found;
}

bool exist(vector<vector<char>>& board, string word) {
    int n = board.size(), m = board[0].size();

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (dfs(board, word, i, j, 0)) return true;
        }
    }

    return false;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n × m × 4^L) (L = word length)
Space Complexity: O(L) recursion stack
## 🔁 Pattern
DFS + Backtracking
Grid Traversal
## 🌍 Real World Use
Puzzle solving (word search games)
Pathfinding in grids

