# [1408. String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array)

Given an array of string `words`, return all strings in `words` that is a
substring of another word. You can return the answer in any order.

A substring is a contiguous sequence of characters within a string.

Constraints:

* `1 <= words.length <= 100`
* `1 <= words[i].length <= 30`
* `words[i]` contains only lowercase English letters.
* All the strings of words are unique.

## Solution

```c++
class Solution {
public:
    std::vector<std::string> stringMatching(std::vector<std::string>& words) {
        std::vector<std::string> ans{};

        int N = words.size();
        if (N == 1) {
            return ans;
        }

        std::ranges::sort(words, {}, &std::string::size);

        for (int i=0; i<N-1; ++i) {
            for (int j=i+1; j<N; ++j) {
                if (words[j].find(words[i]) != std::string::npos) {
                    ans.push_back(words[i]);
                    break;
                }
            }
        }

        return ans;
    }
};
```

## Analysis

Time complexity for sorting is `O(n*logn)` but `O(l*n^2)` worse-case for the
nested for-loops where `l` is the length of the longest string and since
`std::string::find()` is linear.

Space complexity is `O(1)` for in-place sorting and `O(c*n)` for some `c` where
`0 <= c < 1` because all strings are unique.
