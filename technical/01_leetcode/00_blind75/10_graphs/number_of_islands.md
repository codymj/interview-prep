# [200. Number of Islands](https://leetcode.com/problems/number-of-islands)

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land)
and `'0'`s (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands
horizontally or vertically. You may assume all four edges of the grid are all
surrounded by water.

Constraints:

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 300`
* `grid[i][j]` is `'0'` or `'1'`.

## Solution

```c++
class Solution {
private:
    int m_M{};
    int m_N{};

    void visit(int const m, int const n, std::vector<std::vector<char>>& grid) {
        // Boundary check.
        if (m < 0 || m >= m_M || n < 0 || n >= m_N || grid[m][n] != '1') {
            return;
        }

        // Mark coordinate as visited.
        grid[m][n] = '0';

        // Try to visit in each direction.
        visit(m-1, n, grid);
        visit(m+1, n, grid);
        visit(m, n-1, grid);
        visit(m, n+1, grid);
    }

public:
    int numIslands(std::vector<std::vector<char>>& grid) {
        m_M = grid.size();
        m_N = grid[0].size();

        int ans = 0;
        for (int m=0; m<m_M; ++m) {
            for (int n=0; n<m_N; ++n) {
                if (grid[m][n] == '1') {
                    visit(m, n, grid);
                    ans++;
                }
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(M*N)` where `M` is the number of rows in the grid and `N`
is the number of columns.

Space complexity is also `O(M*N)` worst-case if the whole grid is one island.
