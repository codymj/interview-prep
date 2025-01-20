# [2661. First Completely Painted Row or Column](https://leetcode.com/problems/first-completely-painted-row-or-column)

You are given a 0-indexed integer array `arr`, and an `m x n` integer matrix
`mat`. `arr` and `mat` both contain all the integers in the range `[1, m * n]`.

Go through each index `i` in `arr` starting from index `0` and paint the cell in
`mat` containing the integer `arr[i]`.

Return the smallest index `i` at which either a row or a column will be
completely painted in `mat`.

Constraints:

* `m == mat.length`
* `n = mat[i].length`
* `arr.length == m * n`
* `1 <= m, n <= 10^5`
* `1 <= m * n <= 10^5`
* `1 <= arr[i], mat[r][c] <= m * n`
* All the integers of `arr` are unique.
* All the integers of `mat` are unique.

## Solution

```c++
class Solution {
public:
    int firstCompleteIndex(
        std::vector<int>& arr,
        std::vector<std::vector<int>>& mat
    ) {
        int const M = mat.size();
        int const N = mat[0].size();

        // Store coordinates in a vector for O(1) lookup.
        std::vector<std::pair<int,int>> map(M*N);
        for (int i=0; i<M; ++i) {
            for (int j=0; j<N; ++j) {
                map[mat[i][j]-1] = {i, j};
            }
        }

        // Store how many painted cells are in each row and column.
        // Once any row or column is completely painted, return that index i.
        std::vector<int> rowCounts(M, 0);
        std::vector<int> colCounts(N, 0);
        for (int i=0; i<arr.size(); ++i) {
            auto& [r, c] = map[arr[i]-1];
            if (++rowCounts[r] == N || ++colCounts[c] == M) {
                return i;
            }
        }

        return arr.size()-1;
    }
};
```

## Analysis

Time complexity is `O(m*n + m*n)` to create the lookup vector mapping cell
coordinates by the cell value. We can do this since each element is unique. And
an additional `m*n` to iterate over `arr` which reduces to `O(m*n)`.

Space complexity is also `O(m*n)` to store the lookup vector.
