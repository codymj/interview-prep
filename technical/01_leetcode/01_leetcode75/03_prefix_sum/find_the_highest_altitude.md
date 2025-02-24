# [1732. Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude)

There is a biker going on a road trip. The road trip consists of `n + 1` points
at different altitudes. The biker starts his trip on point `0` with altitude
equal `0`.

You are given an integer array gain of length `n` where `gain[i]` is the net
gain in altitude between points `i​​​​​​` and `i + 1` for all `(0 <= i < n)`. Return
the highest altitude of a point.

Constraints:

* `n == gain.length`
* `1 <= n <= 100`
* `-100 <= gain[i] <= 100`

## Solution

```c++
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int const N = gain.size();

        // Iterate over the points.
        // Keep track of the current altitude and max altitude.
        int maxAlt = 0, currentAlt = 0;
        for (int i=0; i<N; ++i) {
            currentAlt += gain[i];
            maxAlt = std::max(maxAlt, currentAlt);
        }

        return maxAlt;
    }
};
```

## Analysis

Time complexity is `O(n)` due to iterating over the points of `gain`.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
