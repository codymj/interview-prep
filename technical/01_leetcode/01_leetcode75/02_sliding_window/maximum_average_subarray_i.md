# [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i)

You are given an integer array `nums` consisting of n elements, and an integer
`k`.

Find a contiguous subarray whose length is equal to `k` that has the maximum
average value and return this value. Any answer with a calculation error less
than `10^-5` will be accepted.

Constraints:

* `n == nums.length`
* `1 <= k <= n <= 10^5`
* `-10^4 <= nums[i] <= 10^4`

## Solution

```c++
class Solution {
public:
    double findMaxAverage(std::vector<int>& nums, int k) {
        int const N = nums.size();

        // Initialize sums with the first k elements.
        double sum = 0, max_sum = 0;
        for (int i=0; i<k; ++i) {
            sum += nums[i];
        }
        max_sum = sum;

        // Iterate over the rest of nums.
        // Remove the i-kth element while adding ith element.
        // Recalculate sums.
        for (int i=k; i<N; ++i) {
            sum += nums[i] - nums[i-k];
            max_sum = std::max(max_sum, sum);
        }

        return max_sum/k;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `nums` once.

Space complexity is `O(1)` since we're not allocating any addiational memory
with respect to input size.
