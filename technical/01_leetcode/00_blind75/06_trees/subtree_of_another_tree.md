# [572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree)

Given the roots of two binary trees `root` and `subRoot`, return `true` if there
is a subtree of `root` with the same structure and node values of `subRoot` and
`false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree`
and all of this node's descendants. The tree `tree` could also be considered as
a subtree of itself.

Constraints:

* The number of nodes in the root tree is in the range `[1, 2000]`.
* The number of nodes in the subRoot tree is in the range `[1, 1000]`.
* `-10^4 <= root.val <= 10^4`
* `-10^4 <= subRoot.val <= 10^4`

## Solution

```c++
class Solution {
public:
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if (!root) {
            // Base case.
            return false;
        } else if (isSameTree(root, subRoot)) {
            // Check if the trees are the same at this point.
            return true;
        } else {
            // Try checking root's children.
            return (
                isSubtree(root->left, subRoot) ||
                isSubtree(root->right, subRoot)
            );
        }
    }

    bool isSameTree(TreeNode* t1, TreeNode* t2) {
        if (!t1 || !t2) {
            // Null checks.
            return !t1 && !t2;
        } else if (t1->val == t2->val) {
            // Ensure subtrees are equal.
            return (
                isSameTree(t1->left, t2->left) &&
                isSameTree(t1->right, t2->right)
            );
        } else {
            return false;
        }
    }
};
```

## Analysis

Time complexity will be `O(m*n)` where `m` is the size of `t1` and `n` is the
size of `t2` since we have to traverse all of `t2` up to `n` times to check for
equality.

Space complexity in the worst-case will be `O(m)` if the trees are linked lists,
otherwise, best-case space complexity is `O(logm)`.
