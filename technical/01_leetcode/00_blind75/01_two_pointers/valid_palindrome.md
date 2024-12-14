# [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome)

A phrase is a **palindrome** if, after converting all uppercase letters into
lowercase letters and removing all non-alphanumeric characters, it reads the
same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

Constraints:

* `1 <= s.length <= 2 * 10^5`
* `s` consists only of printable ASCII characters.

## Solution

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        // Initialize right and left "pointers."
        auto l = 0;
        auto r = s.size()-1;

        // Start pointers at edges and move them towards the middle, skipping
        // non-alphanumeric characters and converting characters to lowercase.
        while (l < r) {
            if (!std::isalnum(s[l])) {
                ++l;
                continue;
            }
            if (!std::isalnum(s[r])) {
                --r;
                continue;
            }

            if (std::tolower(s[l]) != std::tolower(s[r])) {
                return false;
            }
            ++l; --r;
        }

        return true;
    }
};
```

## Analysis

Time complexity is `O(n)` since we iterate over all characters in `s` once.

Space complexity is `O(1)` since we're only comparing characters in `s`
in-place.
