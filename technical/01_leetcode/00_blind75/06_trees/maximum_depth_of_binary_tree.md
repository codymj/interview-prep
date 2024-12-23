# [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path
from the root node down to the farthest leaf node.

Constraints:

* The number of nodes in the tree is in the range `[0, 10^4]`.
* `-100 <= Node.val <= 100`

## Solution

```c++
/*
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
    int maxDepth(TreeNode* root) {
        // Don't add height if the node doesn't exist.
        if (!root) {
            return 0;
        }

        // Traverse each side of subtree and add current node to the max height
        // between the left and right subtrees.
        return 1 + std::max(
            maxDepth(root->left),
            maxDepth(root->right)
        );
    }
};
```

## Analysis

Time complexity is `O(n)` due to having to traverse the entire tree.

Space complexity is `O(n)` worse-case if the tree is a linked list. If the tree
is balanced, then it's `O(logn)`.
