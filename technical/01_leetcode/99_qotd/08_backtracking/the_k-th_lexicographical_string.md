# [1415. The k-th Lexicographical String of All Happy Strings of Length n](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n)

A happy string is a string that:

* consists only of letters of the set `['a', 'b', 'c']`.
* `s[i] != s[i + 1]` for all values of `i` from `1` to `s.length - 1` (string
is 1-indexed).

For example, strings `"abc"`, `"ac"`, `"b"` and `"abcbabcbcb"` are all happy
strings and strings `"aa"`, `"baa"` and `"ababbc"` are not happy strings.

Given two integers `n` and `k`, consider a list of all happy strings of length
`n` sorted in lexicographical order.

Return the kth string of this list or return an empty string if there are less
than `k` happy strings of length `n`.

Constraints:

* `1 <= n <= 10`
* `1 <= k <= 100`

## Solution

```c++
class Solution {
public:
    string getHappyString(int n, int k) {
        std::string current{};
        std::string ans{};
        short count = 0;

        std::function<void()> generate = [&]() -> void {
            // Current string is of size n, increment string count.
            // If at kth string, it is the answer.
            if (current.size() == n) {
                count++;
                if (count == k) {
                    ans = current;
                }
                return;
            }

            // Generate string.
            // If current char equals the last char in current string, continue.
            // Add char to string and continue to generate.
            // If answer has been set, return it.
            // Otherwise, backtrack by removing the last char in current string.
            for (char ch='a'; ch<='c'; ++ch) {
                if (current.size() > 0 && current.back() == ch) {
                    continue;
                }

                current += ch;
                generate();

                if (!ans.empty()) {
                    return;
                }

                current.pop_back();
            }
        };

        // Start generating strings.
        generate();

        return ans;
    }
};
```

## Analysis

Time complexity is `O(3*2^(n-1))` since we initially have three choices: a, b,
or c. After that, we only have two choices since the ith choice cannot be equal
to the i-1 choice.

Space complexity is `O(n)` for stack recursion.
