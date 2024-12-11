# [242. Valid Anagram](https://leetcode.com/problems/valid-anagram)

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and
`false` otherwise.

```c++
class Solution {
public:
    bool isAnagram(std::string s, std::string t) {
        // Base case.
        if (s.size() != t.size()) {
            return false;
        }

        // Since the input is only lowercase English characters, we can use a
        // std::vector<int> of size 26 to hold the characters.
        std::vector<int> v(26,0);

        // Iterate over both strings.
        // Increment char instance of s, decrement char instance of t.
        for (int i=0; i<s.size(); ++i) {
            v[s[i]-'a']++;
            v[t[i]-'a']--;
        }

        // If t is an anagram of s, the vector should contain all 0s.
        for (int i : v) {
            if (i != 0) {
                return false;
            }
        }

        return true;
    }
};
```

## Analysis

Time complexity is `O(n)` since we are iterating over `s` and `t` once and then
iterating over the vector `v` once.

Space complexity is `O(1)` since the size of the vector `v` does not change
regardless of the input sizes of `s` and `t`.
