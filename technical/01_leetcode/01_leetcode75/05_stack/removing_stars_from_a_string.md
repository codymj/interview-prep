# [2390. Removing Stars From a String](https://leetcode.com/problems/removing-stars-from-a-string)

You are given a string `s`, which contains stars `*`.

In one operation, you can:

* Choose a star in `s`.
* Remove the closest non-star character to its left, as well as remove the star
itself.

Return the string after all stars have been removed.

Note:

* The input will be generated such that the operation is always possible.
* It can be shown that the resulting string will always be unique.

Constraints:

* `1 <= s.length <= 10^5`
* `s` consists of lowercase English letters and stars `*`.
* The operation above can be performed on `s`.

## Solution

```c++
class Solution {
public:
    string removeStars(string s) {
        // Add characters to stack if the character is a non-star.
        // If it is a star, pop the last character.
        std::stack<char> stack{};
        for (char ch : s) {
            if (ch == '*') {
                stack.pop();
            }
            else {
                stack.push(ch);
            }
        }

        // Form a new string out of what remains in the stack.
        std::string ans{};
        while (!stack.empty()) {
            ans += stack.top();
            stack.pop();
        }
        std::reverse(ans.begin(), ans.end());

        return ans;
    }
};
```

## Analysis

Time complexity is `O(n)` as we're iterating over the string once and reversing
the string `ans`.

Space complexity is `O(n)` as we're storing at most `n` characters in the stack
and at most `n` characters in the string `ans`.
