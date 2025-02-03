# [3105. Longest Strictly Increasing or Strictly Decreasing Subarray](https://leetcode.com/problems/longest-strictly-increasing-or-strictly-decreasing-subarray/)

You are given an array of integers `nums`. Return the length of the longest
subarray of `nums` which is either strictly increasing or strictly decreasing.

Constraints:

* `1 <= nums.length <= 50`
* `1 <= nums[i] <= 50`

## Solution

```c++
class Solution {
public:
    int longestMonotonicSubarray(std::vector<int>& nums) {
        // Count the number of strictly decreasing and increasing sequences.
        // Keep track of the maximum sequence.
        int incCount = 1, decCount = 1;
        int max = 1;
        for (int i=1; i<nums.size(); ++i) {
            if (nums[i] > nums[i-1]) {
                incCount++;
                decCount = 1;
            }
            else if (nums[i] < nums[i-1]) {
                decCount++;
                incCount = 1;
            }
            else {
                decCount = 1;
                incCount = 1;
            }
            max = std::max(max, std::max(incCount, decCount));
        }

        return max;
    }
};
```

## Analysis

Time complexity is `O(n)` since we have to iterate over the entire input once.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to the input size.
