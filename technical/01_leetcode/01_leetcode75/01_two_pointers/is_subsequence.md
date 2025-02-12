# [392. Is Subsequence](https://leetcode.com/problems/is-subsequence)

Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or
false otherwise.

A subsequence of a string is a new string that is formed from the original
string by deleting some (can be none) of the characters without disturbing the
relative positions of the remaining characters. (i.e., `"ace"` is a subsequence
of `"abcde"` while `"aec"` is not).

Constraints:

* `0 <= s.length <= 100`
* `0 <= t.length <= 10^4`
* `s` and `t` consist only of lowercase English letters.

## Solution

```c++
class Solution {
public:
    bool isSubsequence(std::string s, std::string t) {
        // Empty subsequence doesn't disturb t.
        if (s.size() == 0) {
            return true;
        }

        // Iterate over t.
        // If we find all chars in s, we're done.
        auto sIt = s.begin();
        auto tIt = t.begin();
        for (tIt; tIt!=t.end(); ++tIt) {
            if (*sIt == *tIt) {
                sIt++;
            }
            if (sIt == s.end()) {
                return true;
            }
        }

        return false;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over both `s` and `t` once.

Space complexity is `O(1)` since we're not allocating any additional memory with
respect to input size.
