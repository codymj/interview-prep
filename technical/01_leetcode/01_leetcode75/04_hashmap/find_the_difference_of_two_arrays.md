# [2215. Find the Difference of Two Arrays](https://leetcode.com/problems/find-the-difference-of-two-arrays)

Given two 0-indexed integer arrays `nums1` and `nums2`, return a list `answer`
of size 2 where:

* `answer[0]` is a list of all distinct integers in `nums1` which are not
present in `nums2`.
* `answer[1]` is a list of all distinct integers in `nums2` which are not
present in `nums1`.

Note that the integers in the lists may be returned in any order.

Constraints:

* `1 <= nums1.length, nums2.length <= 1000`
* `-1000 <= nums1[i], nums2[i] <= 1000`

## Solution

```c++
class Solution {
public:
    vector<vector<int>> findDifference(vector<int>& nums1, vector<int>& nums2) {
        // Build hash maps.
        std::unordered_map<int,int> nums1_map{};
        for (int i=0; i<nums1.size(); ++i) {
            nums1_map[nums1[i]]++;
        }
        std::unordered_map<int,int> nums2_map{};
        for (int i=0; i<nums2.size(); ++i) {
            nums2_map[nums2[i]]++;
        }

        // Vector to store answer.
        std::vector<std::vector<int>> ans{};

        // Find unique elements in nums1.
        std::unordered_set<int> nums1_set{};
        for (int n : nums1) {
            if (!nums2_map.contains(n)) {
                nums1_set.insert(n);
            }
        }
        ans.push_back(std::vector<int>{nums1_set.begin(), nums1_set.end()});

        // Find unique elements in nums2.
        std::unordered_set<int> nums2_set{};
        for (int n : nums2) {
            if (!nums1_map.contains(n)) {
                nums2_set.insert(n);
            }
        }
        ans.push_back(std::vector<int>{nums2_set.begin(), nums2_set.end()});

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `nums1` and `nums2` twice.

Space complexity is `O(n)` from storing elements in `nums1` and `nums2` in a
map, set and vector.
