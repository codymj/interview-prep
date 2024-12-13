# [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate)

Given an integer array `nums`, return `true` if any value appears at least twice
in the array, and return `false` if every element is distinct.

```c++
class Solution {
public:
    bool containsDuplicate(std::vector<int>& nums) {
        std::unordered_set<int> set{};

        // Check if num is in set. If so, num is a duplicate.
        // Otherwise, add num to set.
        for (int num : nums) {
            if (set.count(num)) {
                return true;
            }
            set.insert(num);
        }

        return false;
    }
};
```

## Analysis

Time complexity is `O(n)` since we only need to iterate once over `nums`.

Space complexity is `O(n)` as well since we're duplicating each element in
`nums` at most once.

It's possible to have `O(1)` space complexity by sorting `nums` first and then
checking for duplicate elements adjacent to each other, but then time complexity
would be `O(n*logn)`.