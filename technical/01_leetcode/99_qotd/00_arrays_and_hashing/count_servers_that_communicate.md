# [1267. Count Servers that Communicate](https://leetcode.com/problems/count-servers-that-communicate)

You are given a map of a server center, represented as a `m * n` integer matrix
`grid`, where `1` means that on that cell there is a server and `0` means that
it is no server. Two servers are said to communicate if they are on the same row
or on the same column.

Return the number of servers that communicate with any other server.

Constraints:

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m <= 250`
* `1 <= n <= 250`
* `grid[i][j] == 0 or 1`

## Solution

```c++
class Solution {
public:
    int countServers(std::vector<std::vector<int>>& grid) {
        int const M = grid.size();
        int const N = grid[0].size();

        std::vector<int> rowCount(N);
        std::vector<int> colCount(M);
        for (int row=0; row<M; ++row) {
            for (int col=0; col<N; ++col) {
                if (grid[row][col]) {
                    rowCount[col]++;
                    colCount[row]++;
                }
            }
        }

        int count = 0;
        for (int row=0; row<M; ++row) {
            for (int col=0; col<N; ++col) {
                if (grid[row][col]) {
                    count += rowCount[col]>1 || colCount[row]>1;
                }
            }
        }

        return count;
    }
};
```

## Analysis

Time complexity is `O(2*M*N)` since we're iterating over the grid twice which
reduces to `O(M*N)`.

Space complexity is `O(M+N)` to account for the two vectors `rowCount` and
`colCount`.
