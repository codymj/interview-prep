# [3066. Minimum Operations to Exceed Threshold Value II](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii)

You are given a 0-indexed integer array `nums`, and an integer `k`.

You are allowed to perform some operations on `nums`, where in a single
operation, you can:

* Select the two smallest integers `x` and `y` from nums.
* Remove `x` and `y` from nums.
* Insert `(min(x, y) * 2 + max(x, y))` at any position in the array.

Note that you can only apply the described operation if `nums` contains at least
two elements.

Return the minimum number of operations needed so that all elements of the array
are greater than or equal to `k`.

Constraints:

* `2 <= nums.length <= 2 * 10^5`
* `1 <= nums[i] <= 10^9`
* `1 <= k <= 10^9`
* The input is generated such that an answer always exists. That is, there
exists some sequence of operations after which all elements of the array are
greater than or equal to `k`.

## Solution

```c++
class Solution {
public:
    int minOperations(std::vector<int>& nums, int k) {
        // Min heap of long integers due to constraints.
        std::priority_queue<long, std::vector<long>, std::greater<long>> minHeap(
            nums.begin(),
            nums.end()
        );

        // Grab the lowest two integers from the heap.
        // Remove them, and add the requested value.
        // Continue until the lowest integer is >= k.
        int ans = 0;
        long min1 = 0, min2 = 0;
        while (minHeap.top() < k) {
            min1 = minHeap.top(); minHeap.pop();
            min2 = minHeap.top(); minHeap.pop();
            minHeap.push(min1 * 2 + min2);
            ans++;
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n*logn)` due to heap sorting.

Space complexity is `O(n)` to account for copying `nums` into a min heap.
