# [2657. Find the Prefix Common Array of Two Arrays](https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays)

You are given two 0-indexed integer permutations `A` and `B` of length `n`.

A prefix common array of `A` and `B` is an array `C` such that `C[i]` is equal
to the count of numbers that are present at or before the index `i` in both `A`
and `B`.

Return the prefix common array of `A` and `B`.

A sequence of `n` integers is called a permutation if it contains all integers
from `1` to `n` exactly once.

Constraints:

* `1 <= A.length == B.length == n <= 50`
* `1 <= A[i], B[i] <= n`
* It is guaranteed that `A` and `B` are both a permutation of `n` integers.

## Solution

```c++
class Solution {
public:
    std::vector<int> findThePrefixCommonArray(
        std::vector<int>& A,
        std::vector<int>& B
    ) {
        int const N = A.size();

        // Prefix common array.
        std::vector<int> ans(N);

        // Frequency array which keeps track of how many times each integer
        // occurs in both A and B. We can do this because of the narrow
        // conditions for A[i] and B[i] and the uniqueness of each element.
        std::vector<int> freq(N+1, 0);

        // Total number of common elements seen so far.
        int count = 0;

        // Iterate over A and B.
        // Increment the occurance of A[i] and if we've seen it before (i.e. it
        // also exists in B), increment count. Do same for B[i].
        // ans[i] is set to the count tallied so far.
        for (int i=0; i<N; ++i) {
            freq[A[i]]++;
            if (freq[A[i]] == 2) {
                count++;
            }

            freq[B[i]]++;
            if (freq[B[i]] == 2) {
                count++;
            }

            ans[i] = count;
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` due to iterating over `A` and `B` once.

Space complexity is also `O(n)` for the answer arrays `ans` and `freq`.
