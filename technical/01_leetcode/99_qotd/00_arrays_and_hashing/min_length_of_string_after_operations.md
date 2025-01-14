# [3223. Minimum Length of String After Operations](https://leetcode.com/problems/minimum-length-of-string-after-operations)

You are given a string `s`.

You can perform the following process on `s` any number of times:

* Choose an index `i` in the string such that there is at least one character to
the left of index `i` that is equal to `s[i]`, and at least one character to the
right that is also equal to `s[i]`.
* Delete the closest character to the left of index `i` that is equal to `s[i]`.
* Delete the closest character to the right of index `i` that is equal to
`s[i]`.

Return the minimum length of the final string `s` that you can achieve.

Constraints:

* `1 <= s.length <= 2 * 10^5`
* `s` consists only of lowercase English letters.

## Solution

```c++
class Solution {
public:
    int minimumLength(string s) {
        int n = s.size();

        // Count the number of occurances of each character.
        std::array<int, 26> arr{};
        for (int i=0; i<n; ++i) {
            arr[s[i] - 'a']++;
        }

        // All we need to know is if the number of occurances of each character
        // is at least 3. If so, we can perform removal operations.
        // If the number is odd, there will be one occurance left in the string.
        // If even, there will be two left in the string.
        for (int i=0; i<26; ++i) {
            if (arr[i] > 2 && arr[i] % 2 == 1) {
                n -= arr[i] - 1;
            }
            if (arr[i] > 2 && arr[i] % 2 == 0) {
                n -= arr[i] - 2;
            }
        }

        return n;
    }
};
```

## Analysis

Time complexity is `O(n)` due to iterating over `s` once and the array `arr`
once.

Space complexity is `O(26)` which simplifies to `O(1)` (constant time).
