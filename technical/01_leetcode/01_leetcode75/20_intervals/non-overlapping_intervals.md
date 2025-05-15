# [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals)

Given an array of intervals `intervals` where `intervals[i] = [start_i, end_i]`,
return the minimum number of intervals you need to remove to make the rest of
the intervals non-overlapping.

Note that intervals which only touch at a point are non-overlapping. For
example, `[1, 2]` and `[2, 3]` are non-overlapping.

Constraints:

* `1 <= intervals.length <= 10^5`
* `intervals[i].length == 2`
* `-5 * 10^4 <= start_i < end_i <= 5 * 10^4`

## Solution

```c++
class Solution {
public:
    int eraseOverlapIntervals(std::vector<std::vector<int>>& intervals) {
        // Sort.
        std::sort(
            intervals.begin(),
            intervals.end(),
            [](auto const& a, auto const& b) {
                return a[1] < b[1];
            }
        );

        // Iterate over intervals and check if beginning of interval[i] is less
        // than end. If it's not, set end to end of current intervals.
        int end = intervals[0][1];
        int ans = 0;
        for (int i=1; i<intervals.size(); ++i) {
            if (intervals[i][0] < end) {
                ans++;
            }
            else {
                end = intervals[i][1];
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n*logn)` for sorting and `O(n)` for iterating over the
intervals after sorting. Total time complexity is then `O(n + n*logn)`.

Space complexity is `O(1)` since we are not allocating any additional memory
with respect to input size.
