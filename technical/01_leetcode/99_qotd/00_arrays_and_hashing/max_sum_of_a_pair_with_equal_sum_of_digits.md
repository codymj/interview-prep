# [2342. Max Sum of a Pair With Equal Sum of Digits](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits)

You are given a 0-indexed array `nums` consisting of positive integers. You can
choose two indices `i` and `j`, such that `i != j`, and the sum of digits of the
number `nums[i]` is equal to that of `nums[j]`.

Return the maximum value of `nums[i] + nums[j]` that you can obtain over all
possible indices `i` and `j` that satisfy the conditions.

Constraints:

* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^9`

## Solution

```c++
class Solution {
public:
    int maximumSum(std::vector<int>& nums) {
        int const N = nums.size();
        if (N == 1) {
            return -1;
        }

        // Lambda to sum digits in integer.
        auto sumDigits = [](int num) -> int {
            int sum = 0, digit = 0;
            while (num > 0) {
                digit = num % 10;
                sum += digit;
                num /= 10;
            }
            return sum;
        };

        // Array to store all possible sums.
        // INT_MAX = 2147483647 so we can store up to:
        //           0999999999 (9*9 = 81)
        // Add an additional 1 to account for 0-index: 82
        std::array<int, 82> arr{};

        // Iterate over nums.
        // Keep track of the max of nums[i] + nums[j] when sums are equal.
        int max = -1, sum = 0;
        for (int i=0; i<N; ++i) {
            sum = sumDigits(nums[i]);
            if (arr[sum] == 0) {
                arr[sum] = nums[i];
            }
            else {
                max = std::max(max, arr[sum] + nums[i]);
                arr[sum] = std::max(arr[sum], nums[i]);
            }
        }

        return max;
    }
};
```

## Analysis

Time complexity is `O(n)` since we're iterating over `nums` once and the
summation of digits for each `num[i]` isn't a leading factor.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
