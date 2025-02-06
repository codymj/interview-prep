# [1790. Check If One String Swap Can Make Strings Equal](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal)

You are given two strings `s1` and `s2` of equal length. A string swap is an
operation where you choose two indices in a string (not necessarily different)
and swap the characters at these indices.

Return `true` if it is possible to make both strings equal by performing at most
one string swap on exactly one of the strings. Otherwise, return `false`.

Constraints:

* `1 <= s1.length, s2.length <= 100`
* `s1.length == s2.length`
* `s1` and `s2` consist of only lowercase English letters.

## Solution

```c++
class Solution {
public:
    bool areAlmostEqual(string s1, string s2) {
        int const N = s1.size();

        // Iterate over s1 and s2.
        // If we find a difference at s1[i], s2[i], increment diff and store the
        // swappable chars since the next diff must contain those chars else one
        // swap is impossible.
        int diff = 0;
        std::pair<char, char> p{};
        for (int i=0; i<N; ++i) {
            char x = s1[i], y = s2[i];
            if (x != y) {
                diff++;
                if (diff > 2 || (diff==2 && (p.first!=y || p.second!=x))) {
                    return false;
                }
                p = {x, y};
            }
        }

        return diff == 0 || diff == 2;
    }
};
```

## Analysis

Time complexity is `O(n)` since we're iterating over `s1` and `s2` once.

Space complexity is `O(1)` as we're not allocating any additional memory with
respect to input size.
