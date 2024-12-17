# [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array)

Suppose an array of length `n` sorted in ascending order is **rotated** between
`1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

* `[4,5,6,7,0,1,2]` if it was rotated `4` times.
* `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that rotating an array `[a[0], a[1], a[2], ..., a[n-1]]` `1` time results
in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of **unique** elements, return the
*minimum element of this array*.

You must write an algorithm that runs in `O(logn)` time.

Constraints:

* `n == nums.length`
* `1 <= n <= 5000`
* `-5000 <= nums[i] <= 5000`
* All the integers of `nums` are unique.
* `nums` is sorted and rotated between `1` and `n` times.

## Solution

```c++
class Solution {
public:
    int findMin(std::vector<int>& nums) {
        // Left, right and middle pointers.
        int l = 0;
        int r = nums.size()-1;
        int m{};

        // Do binary search until we find minimum.
        while (l<r) {
            m = l+(r-l)/2;
            if (nums[m]<=nums[r]) {
                r = m;
            } else {
                l = m+1;
            }
        }

        return nums[l];
    }
};

```

## Analysis

Time complexity is going to be `O(logn)` due to binary search.

Space complexity is `O(1)` since we do not allocate any additional memory with
respect to the input size.
