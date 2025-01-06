# [1769. Minimum Number of Operations to Move All Balls to Each Box](https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box)

You have `n` boxes. You are given a binary string `boxes` of length `n`, where
`boxes[i]` is `'0'` if the `ith` box is **empty**, and `'1'` if it contains
**one** ball.

In one operation, you can move **one** ball from a box to an adjacent box. Box
`i` is adjacent to box `j` if `abs(i - j) == 1`. Note that after doing so, there
may be more than one ball in some boxes.

Return an array `answer` of size `n`, where `answer[i]` is the **minimum**
number of operations needed to move all the balls to the `ith` box.

Each `answer[i]` is calculated considering the initial state of the boxes.

Constraints:

* `n == boxes.length`
* `1 <= n <= 2000`
* `boxes[i]` is either `'0'` or `'1'`.

## Solution

```c++
class Solution {
public:
    vector<int> minOperations(string boxes) {
        int const N = boxes.size();
        std::vector<int> ans(N, 0);

        int prefixCount = 0, prefixSum = 0;
        int suffixCount = 0, suffixSum = 0;
        for (int i=0; i<N; ++i) {
            ans[i] += prefixCount;
            prefixSum += boxes[i] - '0';
            prefixCount += prefixSum;

            int j = N - 1 - i;
            ans[j] += suffixCount;
            suffixSum += boxes[j] - '0';
            suffixCount += suffixSum;
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over the string `boxes` once.

Space complexity is `O(n)` as we're returning a vector `ans` of size `N`.
