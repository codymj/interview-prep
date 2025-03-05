# [872. Leaf-Similar Trees](https://leetcode.com/problems/leaf-similar-trees)

Consider all the leaves of a binary tree, from left to right order, the values
of those leaves form a leaf value sequence.

For example, in the given tree above, the leaf value sequence is
`(6, 7, 4, 9, 8)`.

Two binary trees are considered leaf-similar if their leaf value sequence is the
same.

Return `true` if and only if the two given trees with head nodes `root1` and
`root2` are leaf-similar.

Constraints:

* The number of nodes in each tree will be in the range `[1, 200]`.
* Both of the given trees will have values in the range `[0, 200]`.

## Solution

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        std::vector<int> leaves1{};
        std::vector<int> leaves2{};

        // DFS function.
        std::function<void(TreeNode*, std::vector<int>&)> dfs =
        [&](TreeNode* node, std::vector<int>& leaves) {
            if (!node) { return; }

            if (!node->left && !node->right) {
                leaves.push_back(node->val);
            }
            else {
                dfs(node->left, leaves);
                dfs(node->right, leaves);
            }
        };

        // Run DFS on each tree, storing the leaf values.
        dfs(root1, leaves1);
        dfs(root2, leaves2);

        // Compare.
        return leaves1 == leaves2;
    }
};
```

## Analysis

Time complexity is `O(n1+n2)` where `n1` is the number of nodes in `root1` and
`n2` is the number of nodes in `root2`.

Average space complexity is `O(h1+h2)` where `h1` is the height of `root1` and
`h2` is the height of `root2` with worst-case being the total nodes in each tree
if they're both singly-linked lists.
