# [2658. Maximum Number of Fish in a Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid)

You are given a 0-indexed 2D matrix `grid` of size `m x n`, where `(r, c)`
represents:

* A land cell if `grid[r][c] = 0`, or
* A water cell containing `grid[r][c]` fish, if `grid[r][c] > 0`.

A fisher can start at any water cell `(r, c)` and can do the following
operations any number of times:

* Catch all the fish at cell `(r, c)`, or
* Move to any adjacent water cell.

Return the maximum number of fish the fisher can catch if he chooses his
starting cell optimally, or 0 if no water cell exists.

An adjacent cell of the cell `(r, c)`, is one of the cells `(r, c+1)`,
`(r, c-1)`, `(r+1, c)` or `(r-1, c)` if it exists.

Constraints:

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 10`
* `0 <= grid[i][j] <= 10`

## Solution

```c++
class Solution {
public:
    int findMaxFish(std::vector<std::vector<int>>& grid) {
        int const N = grid.size();
        int const M = grid[0].size();

        int tmp = 0;
        std::function<int(int i, int j)> dfs = [&](int i, int j) -> int {
            // Bounds checking.
            if (i<0 || i>=N || j<0 || j>=M || grid[i][j] == 0) {
                return 0;
            }

            // Catch fish at this cell; mark cell visited.
            int tmp = grid[i][j];
            grid[i][j] = 0;

            // Try going in all directions.
            tmp += dfs(i-1, j) + dfs(i+1, j) + dfs(i, j-1) + dfs(i, j+1);

            return tmp;
        };

        int ans = 0;
        for (int i=0; i<N; ++i) {
            for (int j=0; j<M; ++j) {
                if (grid[i][j] > 0) {
                    ans = std::max(ans, dfs(i, j));
                }
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(N*M)` where `N*M` is the size of `grid`.

Space complexity is also `O(N*M)` in the worst-case stack depth.
