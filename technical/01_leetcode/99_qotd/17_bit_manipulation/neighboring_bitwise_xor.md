# [2683. Neighboring Bitwise XOR](https://leetcode.com/problems/neighboring-bitwise-xor)

A 0-indexed array `derived` with length `n` is derived by computing the bitwise
XOR (⊕) of adjacent values in a binary array `original` of length `n`.

Specifically, for each index `i` in the range `[0, n - 1]`:

* If `i = n - 1`, then `derived[i] = original[i] ⊕ original[0]`.
* Otherwise, `derived[i] = original[i] ⊕ original[i + 1]`.

Given an array `derived`, your task is to determine whether there exists a valid
binary array `original` that could have formed `derived`.

Return `true` if such an array exists or `false` otherwise.

* A binary array is an array containing only `0`'s and `1`'s.

Constraints:

* `n == derived.length`
* `1 <= n <= 10^5`
* The values in derived are either `0`'s or `1`'s

## Solution

```c++
class Solution {
public:
    bool doesValidArrayExist(std::vector<int>& derived) {
        // XOR-sum for derived is 0 if a valid original array exists.
        // That's because each element is XOR'd twice in the original.
        // (Any number XOR'd with itself is 0).
        return (std::accumulate(derived.begin(), derived.end(), 0)) % 2 == 0;
    }
};
```

## Analysis

Time complexity is `O(n)` since we're iterating over `derived`.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
