# [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string)

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in
both lower and upper cases, more than once.

Constraints:

* `1 <= s.length <= 3 * 10^5`
* `s` consist of printable ASCII characters.

## Solution

```c++
class Solution {
public:
    std::string reverseVowels(std::string s) {
        // Set for containing vowels to check against.
        std::unordered_set<char> vowels = {
            'a', 'A', 'e', 'E', 'i', 'I', 'o', 'O', 'u', 'U'
        };

        // Iterate over s using two pointers, l and r to swap vowels.
        // Move pointers until each point to a vowel and swap them, or until
        // l < r.
        int l = 0, r = s.size()-1;
        char tmp{};
        while (l < r) {
            if (vowels.count(s[l]) && !vowels.count(s[r])) {
                r--;
            }
            else if (!vowels.count(s[l]) && vowels.count(s[r])) {
                l++;
            }
            else if (vowels.count(s[l]) && vowels.count(s[r])) {
                tmp = s[l];
                s[l] = s[r];
                s[r] = tmp;
                l++; r--;
            }
            else {
                l++; r--;
            }
        }

        return s;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `s` once.

Space complexity is `O(1)` due to swapping vowels in `s` directly.
