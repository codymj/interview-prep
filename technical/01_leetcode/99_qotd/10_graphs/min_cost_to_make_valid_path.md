# [1368. Minimum Cost to Make at Least One Valid Path in a Grid](https://leetcode.com/problems/minimum-cost-to-make-at-least-one-valid-path-in-a-grid)

Given an `m x n` grid. Each cell of the grid has a sign pointing to the next
cell you should visit if you are currently in this cell. The sign of
`grid[i][j]` can be:

1. which means go to the cell to the right. (i.e go from `grid[i][j]` to
`grid[i][j + 1]`)
2. which means go to the cell to the left. (i.e go from `grid[i][j]` to
`grid[i][j - 1]`)
3. which means go to the lower cell. (i.e go from `grid[i][j]` to
`grid[i + 1][j]`)
4. which means go to the upper cell. (i.e go from `grid[i][j]` to
`grid[i - 1][j]`)

Notice that there could be some signs on the cells of the grid that point
outside the grid.

You will initially start at the upper left cell `(0, 0)`. A valid path in the
grid is a path that starts from the upper left cell `(0, 0)` and ends at the
bottom-right cell `(m - 1, n - 1)` following the signs on the grid. The valid
path does not have to be the shortest.

You can modify the sign on a cell with `cost = 1`. You can modify the sign on a
cell one time only.

Return the minimum cost to make the grid have at least one valid path.

Constraints:

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 100`
* `1 <= grid[i][j] <= 4`

## Solution

```c++
class Solution {
public:
    int minCost(std::vector<std::vector<int>>& grid) {
        int const M = grid.size();
        int const N = grid[0].size();

        // Direction vectors matching grid[i][j] signs:
        // 1=dirs[0], 2=dirs[1], 3=dirs[2], 4=dirs[3]
        std::vector<std::vector<int>> dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}};

        // Matrix for tracking minimum cost to reach each cell.
        std::vector<std::vector<int>> minCost(M, std::vector<int>(N, INT_MAX));
        minCost[0][0] = 0;

        // Deque for 0-1 BFS.
        // cost=0 moves in front, cost=1 moves in back.
        std::deque<std::pair<int, int>> dq{};
        dq.push_front({0, 0});

        // Boundary check.
        auto isValid = [&](int row, int col) {
            return row>=0 && row<M && col>=0 && col<N;
        };

        // BFS.
        while (!dq.empty()) {
            auto [row, col] = dq.front(); dq.pop_front();

            // Try each direction.
            for (int dir=0; dir<4; ++dir) {
                int nRow = row + dirs[dir][0];
                int nCol = col + dirs[dir][1];
                int cost = (grid[row][col] != (dir+1)) ? 1 : 0;

                // If position is valid and we found a better path:
                if (
                    isValid(nRow, nCol) &&
                    minCost[row][col] + cost < minCost[nRow][nCol]
                ) {
                    minCost[nRow][nCol] = minCost[row][col] + cost;

                    // Add to deque based on cost.
                    if (cost == 1) {
                        dq.push_back({nRow, nCol});
                    }
                    else {
                        dq.push_front({nRow, nCol});
                    }
                }
            }
        }

        return minCost[M-1][N-1];
    }
};
```

## Analysis

Time complexity is `O(M*N)` since each cell is processed for each direction.
Even though BFS is `O(V+E)`, this is a grid problem where there are `M*N`
vertices and each vertex has up to 4 edges, or `O(4*V) = O(4*M*N) = O(M*N)`
which gives `O(V+E) = O(M*N + M*N) = O(2*M*N) or O(M*N)`.

Space complexity is also `O(M*N)` to maintain the `minCost` matrix and deque.
