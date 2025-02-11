# [283. Move Zeroes](https://leetcode.com/problems/move-zeroes)

Given an integer array `nums`, move all `0`'s to the end of it while maintaining
the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

Constraints:

* `1 <= nums.length <= 10^4`
* `-2^31 <= nums[i] <= 2^31 - 1`

## Solution

```c++
class Solution {
public:
    void moveZeroes(std::vector<int>& nums) {
        int const N = nums.size();

        // Iterate over nums.
        // Keep track of the index of the last non-zero element and continue to
        // swap 0s.
        int lastNonZeroIdx = 0;
        for (int i=0; i<N; ++i) {
            if (nums[i] != 0) {
                std::swap(nums[lastNonZeroIdx], nums[i]);
                lastNonZeroIdx++;
            }
        }
    }
};
```

## Analysis

Time complexity is `O(n)` due to iterating over `nums` once.

Space complexity is `O(1)` since we're swapping elements in-place.
