# [1768. Merge Strings Alternately](https://leetcode.com/problems/merge-strings-alternately)

You are given two strings `word1` and `word2`. Merge the strings by adding
letters in alternating order, starting with `word1`. If a string is longer than
the other, append the additional letters onto the end of the merged string.

Return the merged string.

Constraints:

* `1 <= word1.length, word2.length <= 100`
* `word1` and `word2` consist of lowercase English letters.

## Solution

```c++
class Solution {
public:
    std::string mergeAlternately(std::string word1, std::string word2) {
        int const N = std::min(word1.size(), word2.size());

        // Iterate over both strings, up to the minimum size.
        std::string ans{};
        int i = 0;
        for (i; i<N; ++i) {
            ans += word1[i];
            ans += word2[i];
        }

        // Append the rest of the longer string.
        if (word1.size() > word2.size()) {
            ans += word1.substr(i, word1.size());
        }
        else if (word2.size() > word1.size()) {
            ans += word2.substr(i, word2.size());
        }

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over both `word1` and `word2` once.

Space complexity is `O(n)` as well, since we're creating a new string of size
`word1.size() + word2.size()`.
