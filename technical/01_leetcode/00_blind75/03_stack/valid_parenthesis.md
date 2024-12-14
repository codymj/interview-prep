# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`,
`'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

Constraints:

* `1 <= s.length <= 10^4`
* `s consists of parentheses only '()[]{}'`

## Solution

```c++
class Solution {
public:
    bool isValid(std::string s) {
        // Stack to hold characters of s.
        std::stack<char> stack{};

        // Iterate over s.
        // If ch is an opening character, push it onto the stack.
        // Otherwise, make sure the complementary closing character matches the
        // opening character on the top of the stack.
        for (char ch : s) {
            if (
                ch == '(' ||
                ch == '[' ||
                ch == '{'
            ) {
                stack.push(ch);
            } else {
                if (
                    stack.empty() ||
                    stack.top() != '(' && ch == ')' ||
                    stack.top() != '{' && ch == '}' ||
                    stack.top() != '[' && ch == ']'
                ) {
                    return false;
                }
                stack.pop();
            }
        }

        return stack.empty();
    }
};
```

## Analysis

Time complexity is `O(n)` due to iterating over the string `s` once.

Space complexity is `O(n)` since we're storing at most all characters in `s`.
