# [3042. Count Prefix and Suffix Pairs I](https://leetcode.com/problems/count-prefix-and-suffix-pairs-i)

You are given a 0-indexed string array `words`.

Let's define a boolean function `isPrefixAndSuffix` that takes two strings,
`str1` and `str2`:

* `isPrefixAndSuffix(str1, str2)` returns `true` if `str1` is both a prefix and
a suffix of `str2`, and `false` otherwise.

For example, `isPrefixAndSuffix("aba", "ababa")` is `true` because `"aba"` is a
prefix of `"ababa"` and also a suffix, but `isPrefixAndSuffix("abc", "abcd")` is
`false`.

Return an integer denoting the number of index pairs `(i, j)` such that `i < j`,
and `isPrefixAndSuffix(words[i], words[j])` is `true`.

Constraints:

* `1 <= words.length <= 50`
* `1 <= words[i].length <= 10`
* `words[i]` consists only of lowercase English letters.

## Solution

```c++
class Solution {
public:
    int countPrefixSuffixPairs(std::vector<std::string>& words) {
        int ans{};
        for (int i=0; i<words.size()-1; ++i) {
            for (int j=i+1; j<words.size(); ++j) {
                if (isPrefixAndSuffix(words[i], words[j])) {
                    ans++;
                }
            }
        }

        return ans;
    }

    bool isPrefixAndSuffix(std::string str1, std::string str2) {
        if (str1.size() <= str2.size()) {
            size_t found = str2.find(str1);
            size_t rfound = str2.rfind(str1);
            if (found == 0 && rfound == str2.size() - str1.size()) {
                return true;
            }
        }

        return false;
    }
};
```

## Analysis

Time complexity is `O(n^2)` in the worst-case.

Space complexity is `O(1)` as we're not addressing any additional memory with
respect to input size.
