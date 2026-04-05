# 🧩 Number of Islands
## 🧠 Intuition

We need to count number of connected components (islands) in a grid.

## 👉 Key idea:

Use DFS/BFS
When land ('1') is found → explore entire island
## 🐢 Brute Force Approach
Try all possibilities (not practical)
## ⚡ Better Approach (DFS Traversal)
Traverse grid
When '1' found:
Run DFS
Mark visited
🚀 Optimal Approach (DFS / BFS)
DFS
```CPP
#include <vector>
using namespace std;

void dfs(vector<vector<char>>& grid, int i, int j) {
    int n = grid.size();
    int m = grid[0].size();

    if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] == '0') return;

    grid[i][j] = '0'; // mark visited

    dfs(grid, i + 1, j);
    dfs(grid, i - 1, j);
    dfs(grid, i, j + 1);
    dfs(grid, i, j - 1);
}

int numIslands(vector<vector<char>>& grid) {
    int n = grid.size();
    int m = grid[0].size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (grid[i][j] == '1') {
                count++;
                dfs(grid, i, j);
            }
        }
    }

    return count;
}
```
BFS
```CPP
#include <vector>
#include <queue>
using namespace std;

int numIslands(vector<vector<char>>& grid) {
    int n = grid.size();
    int m = grid[0].size();
    int count = 0;

    vector<pair<int,int>> directions = {{1,0},{-1,0},{0,1},{0,-1}};

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (grid[i][j] == '1') {
                count++;
                queue<pair<int,int>> q;
                q.push({i, j});
                grid[i][j] = '0';

                while (!q.empty()) {
                    auto [x, y] = q.front();
                    q.pop();

                    for (auto& d : directions) {
                        int nx = x + d.first;
                        int ny = y + d.second;

                        if (nx >= 0 && ny >= 0 && nx < n && ny < m && grid[nx][ny] == '1') {
                            grid[nx][ny] = '0';
                            q.push({nx, ny});
                        }
                    }
                }
            }
        }
    }

    return count;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n × m)
Space Complexity: O(n × m) (recursion/queue)
## 🔁 Pattern
Graph Traversal (DFS/BFS)
Connected Components
## 🌍 Real World Use
Counting clusters in maps (land/water)
Image segmentation
Network connectivity
