# [1800. Maximum Ascending Subarray Sum](https://leetcode.com/problems/maximum-ascending-subarray-sum)

Given an array of positive integers `nums`, return the maximum possible sum of
an ascending subarray in `nums`.

A subarray is defined as a contiguous sequence of numbers in an array.

A subarray `[numsl, numsl+1, ..., numsr-1, numsr]` is ascending if for all `i`
where `l <= i < r`, `numsi  < nums_(i+1)`. Note that a subarray of size `1` is
ascending.

Constraints:

* `1 <= nums.length <= 100`
* `1 <= nums[i] <= 100`


## Solution

```c++
class Solution {
public:
    int maxAscendingSum(vector<int>& nums) {
        int const N = nums.size();

        // Iterate over nums.
        // Keep track of the previous value to determine ascendancy.
        // Keep adding to sum until ascendancy case fails and note the max.
        int max = 0, sum = 0, pre = 0;
        for (int i=0; i<N; ++i) {
            if (pre < nums[i]) {
                sum += nums[i];
            }
            else {
                sum = nums[i];
            }
            pre = nums[i];
            max = std::max(max, sum);
        }

        return max;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `nums` once.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
