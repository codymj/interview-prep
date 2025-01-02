# [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)

A trie (pronounced as "try") or **prefix tree** is a tree data structure used to
efficiently store and retrieve keys in a dataset of strings. There are various
applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

* `Trie()` Initializes the trie object.
* `void insert(String word)` Inserts the string `word` into the trie.
* `boolean search(String word)` Returns `true` if the string `word` is in the
trie (i.e., was inserted before), and `false` otherwise.
* `boolean startsWith(String prefix)` Returns `true` if there is a previously
inserted string `word` that has the prefix `prefix`, and `false` otherwise.

Constraints:

* `1 <= word.length, prefix.length <= 2000`
* `word` and `prefix` consist only of lowercase English letters.
* At most `3 * 10^4` calls in total will be made to `insert`, `search`, and
`startsWith`.

## Solution

```c++
class TrieNode {
public:
    TrieNode() {}

    bool isWord{};
    std::array<std::unique_ptr<TrieNode>, 26> children{};
};

class Trie {
private:
    std::unique_ptr<TrieNode> m_root;

public:
    Trie() {
        m_root = std::make_unique<TrieNode>();
    }

    void insert(string word) {
        TrieNode* it = m_root.get();

        // Iterate through the trie.
        // If ch is not present, create a node for it.
        char ch;
        for (int i=0; i<word.size(); ++i) {
            ch = word[i];
            if (it->children[ch-'a'].get() == nullptr) {
                it->children[ch-'a'] = std::make_unique<TrieNode>();
            }
            it = it->children[ch-'a'].get();
        }

        // Set isWord flag to indicate this branch forms an inserted word.
        it->isWord = true;
    }

    bool search(string word) {
        TrieNode* it = m_root.get();

        // Iterate through the trie.
        // If ch is not present, the word is not in the trie.
        char ch;
        for (int i=0; i<word.size(); ++i) {
            ch = word[i];
            if (it->children[ch-'a'].get() == nullptr) {
                return false;
            }
            it = it->children[ch-'a'].get();
        }

        // End of branch, return if this branch is an inserted word.
        return it->isWord;
    }

    bool startsWith(string prefix) {
        TrieNode* it = m_root.get();

        // Iterate through the trie.
        // If ch is not present, the prefix is not in the trie.
        char ch;
        for (int i=0; i<prefix.size(); ++i) {
            ch = prefix[i];
            if (it->children[ch-'a'].get() == nullptr) {
                return false;
            }
            it = it->children[ch-'a'].get();
        }

        // Reach the end of the branch, so prefix exists.
        return true;
    }
};

/*
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

## Analysis

* `insert` - Time complexity will be `O(1)` for checking if a node exists for
each character in `word` as well as inserting of a node. Worst case is none of
the characters are inserted into the trie in which case time complexity is
`O(1 * n)` where `n` is the length of `word`. Space complexity for inserting a
node is `O(1)` due to pre-addressing space in the array, so for adding `n` words
of size `s`, the complexity will be `O(n * s)` worst case.
* `search` - Time complexity is `O(1)` for character look ups so total time
complexity is `O(1 * n)` where `n` is length of the word. Space complexity is
obviously `O(1)` as no additional space is used for searching except for a fixed
number of pointers for traversal.
* `startsWith` is similar to `search`, time complexity is `O(n)` where `n` is
the length of `prefix`. Space complexity is also `O(1)`.
