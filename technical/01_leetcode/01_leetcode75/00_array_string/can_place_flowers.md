# [605. Can Place Flowers](https://leetcode.com/problems/can-place-flowers)

You have a long flowerbed in which some of the plots are planted, and some are
not. However, flowers cannot be planted in adjacent plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means
empty and `1` means not empty, and an integer `n`, return `true` if `n` new
flowers can be planted in the `flowerbed` without violating the
no-adjacent-flowers rule and `false` otherwise.

Constraints:

* `1 <= flowerbed.length <= 2 * 10^4`
* `flowerbed[i]` is `0` or `1`.
* There are no two adjacent flowers in flowerbed.
* `0 <= n <= flowerbed.length`

## Solution

```c++
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int const N = flowerbed.size();

        int possible = 0;
        for (int i=0; i<N; ++i) {
            if (flowerbed[i] == 0) {
                // Current plot is empty, check if adjacent plots are empty.
                bool lEmpty = (i == 0) || (flowerbed[i-1] == 0);
                bool rEmpty = (i == flowerbed.size()-1) || (flowerbed[i+1] == 0);

                // If they are, count it as a possible plot and return early if
                // necessary.
                if (lEmpty && rEmpty) {
                    flowerbed[i] = 1;
                    possible++;
                    if (possible >= n) {
                        return true;
                    }
                }
            }
        }

        return possible >= n;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over flowerbed once.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
