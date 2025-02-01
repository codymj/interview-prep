# [1071. Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings)

For two strings `s` and `t`, we say "`t` divides `s`" if and only if
`s = t + t + t + ... + t + t` (i.e., `t` is concatenated with itself one or more
times).

Given two strings `str1` and `str2`, return the largest string `x` such that `x`
divides both `str1` and `str2`.

Constraints:

* `1 <= str1.length, str2.length <= 1000`
* `str1` and `str2` consist of English uppercase letters.

## Solution

```c++
class Solution {
public:
    std::string gcdOfStrings(std::string str1, std::string str2) {
        // If one string divides the other, they'll be commutative.
        if (str1 + str2 != str2 + str1) {
            return "";
        }

        // Calculate GCD.
        int gcd = calcGcd(str1.size(), str2.size());

        // Since the strings are commutative, the substring from position 0 to
        // GCD should divide both str1 and str2 though we only need to check
        // one.
        return str1.substr(0, gcd);
    }

    // Calculates GCD between two integers (Euclid's method).
    int calcGcd(int n1, int n2) {
        int tmp{};
        while (n2 != 0) {
            tmp = n1 % n2;
            n1 = n2;
            n2 = tmp;
        }

        return n1;
    }
};
```

## Analysis

Time complexity is `O(m+n)` where `m` is `str1.size()` and `n` is `str2.size()`.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
