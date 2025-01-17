# [2425. Bitwise XOR of All Pairings](https://leetcode.com/problems/bitwise-xor-of-all-pairings)

You are given two 0-indexed arrays, `nums1` and `nums2`, consisting of
non-negative integers. There exists another array, `nums3`, which contains the
bitwise XOR of all pairings of integers between `nums1` and `nums2` (every
integer in `nums1` is paired with every integer in `nums2` exactly once).

Return the bitwise XOR of all integers in `nums3`.

Constraints:

* `1 <= nums1.length, nums2.length <= 10^5`
* `0 <= nums1[i], nums2[j] <= 10^9`

## Solution

```c++
class Solution {
public:
    int xorAllNums(std::vector<int>& nums1, std::vector<int>& nums2) {
        int const N = nums1.size();
        int const M = nums2.size();

        // Each element in nums1 appears M times.
        // If M is even, the result of xor1 would be 0.
        // So, only need to XOR if M is odd.
        int xor1{};
        if (M % 2) {
            for (int num : nums1) {
                xor1 ^= num;
            }
        }

        // Each element in nums2 appears N times.
        // If N is even, the result of xor2 would be 0.
        // So, only need to XOR if N is odd.
        int xor2{};
        if (N % 2) {
            for (int num : nums2) {
                xor2 ^= num;
            }
        }

        return xor1 ^ xor2;
    }
};
```

## Analysis

Time complexity is `O(n + m)` where `n` is the size of `nums1.size()` and `m` is
`nums2.size()` since we're iterating over both `nums1` and `nums2`.

Space complexity is `O(1)` since we are not allocating any additional memory
with respect to input size.
