# [2206. Divide Array Into Equal Pairs](https://leetcode.com/problems/divide-array-into-equal-pairs)

You are given an integer array `nums` consisting of `2 * n` integers.

You need to divide `nums` into `n` pairs such that:

* Each element belongs to exactly one pair.
* The elements present in a pair are equal.

Return `true` if nums can be divided into `n` pairs, otherwise return `false`.

Constraints:

* `nums.length == 2 * n`
* `1 <= n <= 500`
* `1 <= nums[i] <= 500`

## Solution

```c++
class Solution {
public:
    bool divideArray(vector<int>& nums) {
        // Bitset to check polarity of each element in nums.
        std::bitset<500> bitset{};
        for (int num : nums) {
            bitset.flip(num-1);
        }

        // All bits should be 0 for even polarity.
        return bitset.none();
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `nums` once.

Space complexity is `O(1)` by leveraging the second constraint.
