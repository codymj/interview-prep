[2185. Counting Words With a Given Prefix](https://leetcode.com/problems/counting-words-with-a-given-prefix)

You are given an array of strings `words` and a string `pref`.

Return the number of strings in `words` that contain `pref` as a prefix.

A prefix of a string `s` is any leading contiguous substring of `s`.

Constraints:

* `1 <= words.length <= 100`
* `1 <= words[i].length, pref.length <= 100`
* `words[i]` and `pref` consist of lowercase English letters.

## Solution

```c++
class Solution {
public:
    int prefixCount(std::vector<std::string>& words, std::string pref) {
        int ans{};

        // Iterate over words.
        // Only need to check range [0, pref.size()) for a match as opposed to
        // using std::string::find() which will continue searching the entire
        // string.
        for (int i=0; i<words.size(); ++i) {
            if (words[i].substr(0, pref.size()) == pref) {
                ans++;
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity will be `O(n*m)` where `n` is size of `words[i]` and `m` is the
size of `pref`.

Space complexity is `O(1)` as there is no additional memory used with respect to
the input size.
