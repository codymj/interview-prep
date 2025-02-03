# [1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies)

There are `n` kids with candies. You are given an integer array `candies`, where
each `candies[i]` represents the number of candies the `ith` kid has, and an
integer `extraCandies`, denoting the number of extra candies that you have.

Return a boolean array `result` of length n, where `result[i]` is `true` if,
after giving the `ith` kid all the `extraCandies`, they will have the greatest
number of candies among all the kids, or `false` otherwise.

Note that multiple kids can have the greatest number of candies.

Constraints:

* `n == candies.length`
* `2 <= n <= 100`
* `1 <= candies[i] <= 100`
* `1 <= extraCandies <= 50`

## Solution

```c++
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
        int const N = candies.size();

        // Find the maximum candies at least one kid has.
        int max = 0;
        for (int i=0; i<N; ++i) {
            max = std::max(max, candies[i]);
        }

        // Iterate over each kid again, but check if the ith kid now has the max
        // number of candies after giving them the extra candies.
        std::vector<bool> ans(N, false);
        for (int i=0; i<N; ++i) {
            if (candies[i] + extraCandies >= max) {
                ans[i] = true;
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over the list of candies twice.

Space complexity is also `O(n)` since our answer is a `std::vector` of size
equal to the input `candies`.
