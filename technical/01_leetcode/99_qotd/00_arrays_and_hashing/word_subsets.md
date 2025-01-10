# [916. Word Subsets](https://leetcode.com/problems/word-subsets)

You are given two string arrays `words1` and `words2`.

A string `b` is a subset of string `a` if every letter in `b` occurs in `a`
including multiplicity.

For example, `"wrr"` is a subset of `"warrior"` but is not a subset of
`"world"`.

A string a from `words1` is universal if for every string `b` in `words2`, `b`
is a subset of `a`.

Return an array of all the universal strings in `words1`. You may return the
answer in any order.

Constraints:

* `1 <= words1.length, words2.length <= 10^4`
* `1 <= words1[i].length, words2[i].length <= 10`
* `words1[i]` and `words2[i]` consist only of lowercase English letters.
* All the strings of `words1` are unique.

## Solution

```c++
class Solution {
public:
    std::vector<std::string> wordSubsets(
        std::vector<std::string>& words1,
        std::vector<std::string>& words2
    ) {
        // Calculate the max frequency of each character, in each word of
        // words2.
        std::array<int, 26> maxFreq{};
        for (std::string const& word : words2) {
            std::array<int, 26> freq{};
            for (char const c : word) {
                freq[c-'a']++;
            }
            for (int i=0; i<26; ++i) {
                maxFreq[i] = std::max(maxFreq[i], freq[i]);
            }
        }

        // For each word in words1, calculate the frequency of each character
        // and check universality.
        std::vector<string> ans{};
        ans.reserve(words1.size());
        for (std::string const& word : words1) {
            std::array<int, 26> freq{};
            for (char const c : word) {
                freq[c-'a']++;
            }
            if (isUniversal(freq, maxFreq)) {
                ans.push_back(word);
            }
        }

        return ans;
    }

    // Each character in the frequency array must be at least the max frequency
    // for that character.
    bool isUniversal(
        std::array<int, 26> const& wordFreq,
        std::array<int, 26> const& maxFreq
    ) {
        for (int i=0; i<26; ++i) {
            if (wordFreq[i] < maxFreq[i]) {
                return false;
            }
        }

        return true;
    }
};
```

## Analysis

Time complexity is `O(m*l + n*k)` where `m` is `words1.size()` and `l` is the
average length of words in `words1` and checking universality of `words1` for
`n` words of average length `k`.

Space complexity is `O(1)` due to not having to allocate additional memory with
respect to input size.
