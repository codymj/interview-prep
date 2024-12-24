# [100. Same Tree](https://leetcode.com/problems/same-tree)

Given the roots of two binary trees `p` and `q`, write a function to check if
they are the same or not.

Two binary trees are considered the same if they are structurally identical, and
the nodes have the same value.

Constraints:

* The number of nodes in both trees is in the range `[0, 100]`.
* `-10^4 <= Node.val <= 10^4`

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p || !q) {
            // Null checks.
            return !p && !q;
        } else if (p->val == q->val) {
            // Ensure subtrees are equal.
            return(
                isSameTree(p->left, q->left) &&
                isSameTree(p->right, q->right)
            );
        } else {
            return false;
        }
    }
};
```

## Analysis

Time complexity is `O(n)` due to having to traverse the entire tree.

Space complexity is `O(n)` in the worst-case if the tree is a linked list, else
best-case it is `O(logn)` when the tree is balanced.
