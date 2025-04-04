# [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array)

Given an integer array `nums` and an integer `k`, return the kth largest element
in the array.

Note that it is the kth largest element in the sorted order, not the kth
distinct element.

Can you solve it without sorting?

Constraints:

* `1 <= k <= nums.length <= 10^5`
* `-10^4 <= nums[i] <= 10^4`

## Solution

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        // Build min heap to store kth largest elements.
        // Keep only the kth largest elements in the heap.
        std::priority_queue<int, std::vector<int>, std::greater<int>> pq{};
        for (int n : nums) {
            pq.push(n);
            if (pq.size() > k) {
                pq.pop();
            }
        }

        return pq.top();
    }
};
```

## Analysis

Time complexity will be `O(nlogk)` since each removal of the heap is `logk` and
we're iterating over `n` elements.

Space complexity is `O(k)` since we're only storing `k` elements at a time in
the heap.
