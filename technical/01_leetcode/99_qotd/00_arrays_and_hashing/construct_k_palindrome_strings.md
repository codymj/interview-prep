# [1400. Construct K Palindrome Strings](https://leetcode.com/problems/construct-k-palindrome-strings)

Given a string `s` and an integer `k`, return `true` if you can use all the
characters in `s` to construct `k` palindrome strings or `false` otherwise.

Constraints:

* `1 <= s.length <= 10^5`
* `s` consists of lowercase English letters.
* `1 <= k <= 10^5`

## Solution

```c++
class Solution {
public:
    bool canConstruct(std::string s, int k) {
        // Can't create k palindromes with less than k characters.
        if (s.size() < k) {
            return false;
        }

        // Count the number of odd character instances.
        std::bitset<26> arr{};
        for (char const ch : s) {
            arr.flip(ch - 'a');
        }

        // If odd characters > k, then the min number of palindromes is > k
        // (false). Else, exactly k palindromes can be created (true).
        return arr.count() <= k;
    }
};
```

## Analysis

Time complexity is `O(n)` as we iterate over `s`.

Space complexity is `O(1)`.
