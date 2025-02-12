# [1910. Remove All Occurrences of a Substring](https://leetcode.com/problems/remove-all-occurrences-of-a-substring)

Given two strings `s` and `part`, perform the following operation on `s` until
all occurrences of the substring `part` are removed:

* Find the leftmost occurrence of the substring `part` and remove it from `s`.

Return `s` after removing all occurrences of `part`.

A substring is a contiguous sequence of characters in a string.

Constraints:

* `1 <= s.length <= 1000`
* `1 <= part.length <= 1000`
* `s​​​​​​` and `part` consists of lowercase English letters.

## Solution

```c++
class Solution {
public:
    std::string removeOccurrences(std::string s, std::string part) {
        // Iterate over s. Find first occurance of substring and delete it.
        // Repeat until there are no more occurances.
        size_t pos = 0;
        while (true) {
            pos = s.find(part);
            if (pos == std::string::npos) {
                break;
            }
            s.erase(pos, part.size());
        }

        return s;
    }
};
```

## Analysis

Time complexity is `O(m*n)` where `m` is `s.size()` and `n` is `part.size()`.

Space complexity is `O(1)` since we're not allocating any additional memory with
respect to input size.
