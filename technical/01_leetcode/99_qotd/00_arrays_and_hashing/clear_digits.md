# [3174. Clear Digits](https://leetcode.com/problems/clear-digits)

You are given a string `s`.

Your task is to remove all digits by doing this operation repeatedly:

* Delete the first digit and the closest non-digit character to its left.

Return the resulting string after removing all digits.

Constraints:

* `1 <= s.length <= 100`
* `s` consists only of lowercase English letters and digits.
* The input is generated such that it is possible to delete all digits.

## Solution

```c++
class Solution {
public:
    std::string clearDigits(std::string s) {
        int const N = s.size();

        // Use a queue to keep track of element indicies which are digits.
        std::queue<int> idx{};
        for (int i=0; i<N; ++i) {
            if (std::isdigit(s[i])) {
                idx.push(i);
            }
        }

        // Return fast if no digits in s.
        if (idx.size() == 0) {
            return s;
        }

        // Grab each index from the queue.
        // Remove that index in s, along with the element to the left of it.
        // Since we're beginning from the left most digit in s, the element to
        // the left is guaranteed to be a non-digit unless it's the first char.
        int i = 0, offset = 0;
        while (idx.size() > 0) {
            i = idx.front(); idx.pop();
            i -= offset;
            if (i > 0) {
                s.erase(i-1, 2);
                offset += 2;
            }
            else if (i == 0) {
                s.erase(i, 1);
                offset++;
            }
        }

        return s;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over `s` once to locate each digit
and then over the queue `idx` where `idx.size() < s.size()`.

Space complexity is `O(n)` since we're storing up to, but not including
`s.size()` digits.
