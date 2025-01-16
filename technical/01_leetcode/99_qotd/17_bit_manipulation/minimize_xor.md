# [2429. Minimize XOR](https://leetcode.com/problems/minimize-xor)

Given two positive integers `num1` and `num2`, find the positive integer `x`
such that:

* x has the same number of set bits as num2, and
* The value `x XOR num1` is minimal.

Note that XOR is the bitwise XOR operation.

Return the integer `x`. The test cases are generated such that `x` is uniquely
determined.

The number of set bits of an integer is the number of `1`'s in its binary
representation.

Constraints:

* `1 <= num1, num2 <= 10^9`

## Solution

```c++
class Solution {
public:
    int minimizeXor(int num1, int num2) {
        // Count the number of set bits in each int.
        int bitsNum1 = std::bitset<32>(num1).count();
        int bitsNum2 = std::bitset<32>(num2).count();

        // If the number of 1-bits match, return num1 directly
        if (bitsNum1 == bitsNum2) {
            return num1;
        }

        // Start by setting ans to num1.
        int ans = num1;

        // Iterate over bits of num1 starting at the least significant bit.
        for (int i=0; i<32; ++i) {
            // Case 1: Reduce 1-bits if bitsNum1 > bitsNum2.
            if (bitsNum1 > bitsNum2 && (1 << i) & num1) {
                ans ^= 1 << i;
                bitsNum1--;
            }

            // Case 2: Add 1-bits if bitsNum1 < bitsNum2.
            if (bitsNum1 < bitsNum2 && !((1 << i) & num1)) {
                ans ^= 1 << i;
                bitsNum1++;
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(1)` since we're iterating over at most 32 bits and all
inputs are identical in size.

Space complexity is also `O(1)` as we're not allocating any additional memory
with respect to input size.
