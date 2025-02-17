# [1079. Letter Tile Possibilities](https://leetcode.com/problems/letter-tile-possibilities)

You have `n` tiles, where each tile has one letter `tiles[i]` printed on it.

Return the number of possible non-empty sequences of letters you can make using
the letters printed on those `tiles`.

Constraints:

* `1 <= tiles.length <= 7`
* `tiles` consists of uppercase English letters.

## Solution

```c++
class Solution {
public:
    int numTilePossibilities(string tiles) {
        // Frequency of tiles (A-Z).
        std::array<int, 26> tileFreq{};
        for (char c : tiles) {
            tileFreq[c - 'A']++;
        }

        // Function for finding all possible permutations of tiles.
        std::function<int()> calcPossibilities = [&]() -> int {
            int total = 0;

            // Use each available character.
            // Recursively generate a sequence.
            // Backtrack to restore the count.
            for (int tile=0; tile<26; ++tile) {
                if (tileFreq[tile] != 0) {
                    total++;
                    tileFreq[tile]--;
                    total += calcPossibilities();
                    tileFreq[tile]++;
                }
            }

            return total;
        };

        return calcPossibilities();
    }
};
```

## Analysis

Time complexity is `O(2^n)` due to exponential branching when choosing each
character.

Space complexity is `O(26)` for storing tile counts from `A` to `Z` and `O(n)`
for the recursive stack depth so total space complexity is
`O(26) + O(n) = O(1) + O(n) = O(n)`.
