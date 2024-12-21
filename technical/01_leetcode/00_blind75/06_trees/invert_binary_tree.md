# [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree)

Given the `root` of a binary tree, invert the tree, and return *its root*.

Constraints:

* The number of nodes in the tree is in the range `[0, 100]`.
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
    TreeNode* invertTree(TreeNode* root) {
        // If root isn't nullptr, swap its children and add the calls to invert
        // its subtrees to the call stack.
        if (root) {
            std::swap(root->left, root->right);
            invertTree(root->left);
            invertTree(root->right);
        }

        // If root is nullptr, return.
        // The initial call will execute last and return the root of the tree.
        return root;
    }
};
```

## Analysis

Time complexity is `O(n)` since we must traverse the entire tree.

Space complexity is `O(n)` in the worst case if the tree is a singly-linked list
sine we will be adding every node to the call stack. If the tree is balanced, it
will result in an `O(logn)` space complexity due to calls getting executed and
popped off the call stack as the inverting progresses, thus the call stack only
ever grows to at most `logn` size or the height of the tree.
