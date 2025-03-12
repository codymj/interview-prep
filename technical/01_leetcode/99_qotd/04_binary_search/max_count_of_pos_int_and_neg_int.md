# [2529. Maximum Count of Positive Integer and Negative Integer](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer)

Given an array `nums` sorted in non-decreasing order, return the maximum between
the number of positive integers and the number of negative integers.

In other words, if the number of positive integers in `nums` is `pos` and the
number of negative integers is `neg`, then return the maximum of `pos` and
`neg`.

Note that `0` is neither positive nor negative.

Constraints:

* `1 <= nums.length <= 2000`
* `-2000 <= nums[i] <= 2000`
* `nums` is sorted in a non-decreasing order.

## Solution

```c++
class Solution {
public:
    int maximumCount(std::vector<int>& nums) {
        int const N = nums.size();

        // Upper bound of integers less than 0 using binary search.
        auto negUpperBound = [&](std::vector<int> const& vec) -> int {
            int l = 0, r = N-1, m = 0;
            while (l <= r) {
                m = l+((r-l)/2);
                if (vec[m] < 0) {
                    l = m+1;
                }
                else if (vec[m] >= 0) {
                    r = m-1;
                }
            }

            return l;
        };

        // Lower bound of integers greater than 0 using binary search.
        auto posLowerBound = [&](std::vector<int> const& vec) -> int {
            int l = 0, r = N-1, m = 0;
            while (l <= r) {
                m = l+((r-l)/2);
                if (vec[m] <= 0) {
                    l = m+1;
                }
                else if (vec[m] > 0) {
                    r = m-1;
                }
            }

            return l;
        };

        // Return maximum count of either negative or positive integers.
        return std::max(negUpperBound(nums), N-posLowerBound(nums));
    }
};
```

## Analysis

Time complexity is `O(logn)` for finding the bounds.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
