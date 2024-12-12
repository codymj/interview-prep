# [1. Two Sum](https://leetcode.com/problems/two-sum)

Given an array of integers `nums` and an integer `target`, return indices of the
two numbers such that they add up to `target`.

You may assume that each input would have ***exactly*** **one solution**, and
you may not use the same element twice.

You can return the answer in any order.

```c++
class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
        // We can use a regular unordered map since we're guaranteed exactly one
        // solution. If multiples were allowed, we'd need a multimap.
        std::unordered_map<int,int> map{};

        // Iterate over the vector.
        // Calculate the diff of target and nums[i] and then check if that
        // number exists in the map. If not, add that element to the map, mapped
        // to its index. If it exists in the map, return that elements index
        // along with i (the index of the other element which sums to target).
        int diff{};
        for (int i=0; i<nums.size(); ++i) {
            diff = target - nums[i];
            if (map.count(diff)) {
                return std::vector<int>{map[diff], i};
            }
            map.insert({nums[i], i});
        }

        // Formality due to guarantee of a solution.
        return std::vector<int>{};
    }
};
```

## Analysis

Time complexity is `O(n)` since we only iterate over the vector once, and map
lookups are `O(1)` so iteration dominates.

Space complexity is also `O(n)` due to having to store up to the number of
elements in `nums`.
