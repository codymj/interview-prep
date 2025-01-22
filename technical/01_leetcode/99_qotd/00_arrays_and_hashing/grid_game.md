# [2017. Grid Game](https://leetcode.com/problems/grid-game)

You are given a 0-indexed 2D array `grid` of size `2 x n`, where `grid[r][c]`
represents the number of points at position `(r, c)` on the matrix. Two robots
are playing a game on this matrix.

Both robots initially start at `(0, 0)` and want to reach `(1, n-1)`. Each robot
may only move to the right (`(r, c) to (r, c + 1)`) or down
(`(r, c) to (r + 1, c)`).

At the start of the game, the first robot moves from `(0, 0)` to `(1, n-1)`,
collecting all the points from the cells on its path. For all cells `(r, c)`
traversed on the path, `grid[r][c]` is set to `0`. Then, the second robot moves
from `(0, 0)` to `(1, n-1)`, collecting the points on its path. Note that their
paths may intersect with one another.

The first robot wants to minimize the number of points collected by the second
robot. In contrast, the second robot wants to maximize the number of points it
collects. If both robots play optimally, return the number of points collected
by the second robot.

Constraints:

* `grid.length == 2`
* `n == grid[r].length`
* `1 <= n <= 5 * 10^4`
* `1 <= grid[r][c] <= 10^5`

## Solution

```c++
class Solution {
public:
    using ll = long long;
    long long gridGame(std::vector<std::vector<int>>& grid) {
        int const N = grid[0].size();

        // Initialized as the sum of all cells in the top row excluding the
        // first column since robot 1 starts at column 0.
        ll row0 = std::accumulate(grid[0].begin()+1, grid[0].end(), 0LL);

        // Initialized as 0, representing the sum of cells collected by robot 2
        // in the bottom row before robot 1 transitions.
        ll row1 = 0LL;

        ll ans = row0;
        for (int i=1; i<N; ++i) {
            // Subtract the value of grid[0][i] because robot 1 moves past
            // column i, leaving it for robot 2.
            row0 -= grid[0][i];

            // Add the value of grid[1][i-1] because robot 1 transitions to row
            // 1 at column i, leaving the previous cell in row 1 for robot 2.
            row1 += grid[1][i-1];

            // Store the minimum value of max(row0, row1) across all columns.
            ans = std::min(ans, std::max(row0, row1));
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` since the algorithm iterates over all columns once.

Space complexity is `O(1)` as we do not allocate any additional memory with
respect to input size.
