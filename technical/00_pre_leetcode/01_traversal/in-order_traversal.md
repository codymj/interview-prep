# In-Order Traversal

In-order traversal is a depth-first tree traversal method where nodes are
visited in the following order:

1. Left (traverse the left subtree).
2. Root (visit the current node).
3. Right (traverse the right subtree).

It is often used to retrieve nodes in non-decreasing order for binary search
trees and can be recursive or iterative.

## Recursive

```c++
struct Node {
    int value;
    Node* left;
    Node* right;
};

void preOrder(Node* root) {
    if (!root) {
        return;
    }

    // Traverse left, visit current, traverse right.
    preOrder(root->left);
    std::cout << node->value << std::endl;
    preOrder(root->right);
}
```

## Iterative

```c++
struct Node {
    int value;
    Node* left;
    Node* right;
};
std::stack<Node*> stack;

void inOrder(Node *root) {
    Node* current = root;
    while (current || !stack.empty()) {
        // Push nodes onto stack while traversing to the leftmost node.
        while (current) {
            stack.push(current);
            current = current->left;
        }

        // Process current node.
        Node* current = stack.top(); stack.pop();
        std::cout << node->value << std::endl;

        // Explore the right subtree.
        if (current->right) {
            stack.push(current->right);
        }
    }
}
```
