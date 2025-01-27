# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can
you climb to the top?

Constraints:

* `1 <= n <= 45`

## Solution

```c++
class Solution {
public:
    int climbStairs(int n) {
        return nthFib(n) + nthFib(n-1);
    }

    // Return the nth Fibonacci number.
    int nthFib(int n) {
        // Base case.
        if (n <= 0) {
            return 0;
        }

        // Calculate the Fibonacci numbers up to the nth one.
        // Using a bottom-up approach for efficient memory usage.
        int prevFib = 0, currFib = 1, newFib = 0;
        for (int i=1; i<n; ++i) {
            newFib = prevFib + currFib;
            prevFib = currFib;
            currFib = newFib;
        }

        return currFib;
    }
};
```

## Analysis

Time complexity is `O(n)` as we need to calculate the nth Fibonacci number.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
