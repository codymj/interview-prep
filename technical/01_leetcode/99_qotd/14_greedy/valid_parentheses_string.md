# [2116. Check if a Parentheses String Can Be Valid](https://leetcode.com/problems/check-if-a-parentheses-string-can-be-valid)

A parentheses string is a non-empty string consisting only of `'('` and `')'`.
It is valid if any of the following conditions is true:

* It is `()`.
* It can be written as `AB`, where `A` and `B` are valid parentheses strings.
* It can be written as `(A)`, where `A` is a valid parentheses string.

You are given a parentheses string `s` and a string `locked`, both of length
`n`. `locked` is a binary string consisting only of `'0'`s and `'1'`s. For each
index `i` of locked,

* If `locked[i]` is `'1'`, you cannot change `s[i]`.
* But if `locked[i]` is '0', you can change `s[i]` to either `'('` or `')'`.

Return `true` if you can make `s` a valid parentheses string. Otherwise, return
`false`.

Constraints:

* `n == s.length == locked.length`
* `1 <= n <= 10^5`
* `s[i]` is either `'('` or `')'`.
* `locked[i]` is either `'0'` or `'1'`.

## Solution

```c++
class Solution {
public:
    bool canBeValid(std::string s, std::string locked) {
        // If s.size() is odd, it cannot be valid.
        int const N = s.size();
        if (N % 2 == 1) {
            return false;
        }

        // a is the minimum number of '(' at current position (a >= 0).
        // b is the maximum number of '(' at current position.
        int a = 0; int b = 0;
        for (int i=0; i<N; ++i) {
            // If it's '(', increment both a and b.
            // If it's ')', decrement b and ensure a does not drop below 0
            // since ')' can close a previous '('.
            if (locked[i] == '1') {
                if (s[i] == '(') {
                    a++; b++;
                } else {
                    a = std::max(0, a-1);
                    b--;
                }
            }
            // The character can act as either '(' or ')'.
            else {
                a = std::max(0, a-1);
                b++;
            }

            // s is invalid as there's no way to close all open parentheses.
            if (b < 0) {
                return false;
            }
        }

        // If minimum possible open parentheses count is zero, all are closed.
        return a == 0;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `s` once.

Space complexity is `O(1)` as we allocate no additional memory with respect to
input size.
