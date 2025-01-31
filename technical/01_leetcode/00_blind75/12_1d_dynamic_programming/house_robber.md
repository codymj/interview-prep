# [198. House Robber](https://leetcode.com/problems/house-robber)

You are a professional robber planning to rob houses along a street. Each house
has a certain amount of money stashed, the only constraint stopping you from
robbing each of them is that adjacent houses have security systems connected and
it will automatically contact the police if two adjacent houses were broken into
on the same night.

Given an integer array `nums` representing the amount of money of each house,
return the maximum amount of money you can rob tonight without alerting the
police.

Constraints:

* 1 <= nums.length <= 100
* 0 <= nums[i] <= 400

## Solution

```c++
class Solution {
public:
    int rob(std::vector<int>& nums) {
        // Iterate over mem and nums.
        // Two choices to make (pick the max of the two):
        // a) don't rob this house + keep total loot up to this point.
        // b) rob this house + keep total loot from before the previous house.
        int pre = 0, max = 0, tmp = 0;
        for (int num : nums) {
            tmp = max;
            max = std::max(max, pre + num);
            pre = tmp;
        }

        return max;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `nums`.

Space complexity is `O(1)` since we're not allocating any additional memory with
respect to input size.
