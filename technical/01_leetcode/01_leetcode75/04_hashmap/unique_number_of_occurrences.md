# [1207. Unique Number of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences)

Given an array of integers `arr`, return `true` if the number of occurrences of
each value in the array is unique or `false` otherwise.

Constraints:

* `1 <= arr.length <= 1000`
* `-1000 <= arr[i] <= 1000`

## Solution

```c++
class Solution {
public:
    bool uniqueOccurrences(vector<int>& arr) {
        // Map to store frequency of each element.
        std::unordered_map<int,int> map{};
        for (int i=0; i<arr.size(); ++i) {
            map[arr[i]]++;
        }

        // Set to store frequency of each element.
        std::unordered_set<int> set{};
        for (auto const& [k,v] : map) {
            set.insert(v);
        }

        // If frequencies are unique, the sizes should be equal.
        return map.size() == set.size();
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over all elements in `arr` once and
then over all of the occurrences in `set` once.

Space complexity is `O(n)` as we're storing element occurrence frequency in a
map and set.
