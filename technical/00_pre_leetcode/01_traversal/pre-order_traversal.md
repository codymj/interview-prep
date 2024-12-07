# Pre-Order Traversal

Pre-order traversal is a depth-first tree traversal method that visits nodes in
the following order:

1. Root (visit the current node).
2. Left (traverse the left subtree).
3. Right (traverse the right subtree).

It is commonly used to process nodes in hierarchical order or serialize a tree
and can be recursive or iterative.

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

    // Visit current, traverse left, traverse right.
    std::cout << node->value << std::endl;
    preOrder(root->left);
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

void preOrder(Node *root) {
    if (!root) {
        return;
    }
    stack.push(root);

    while (!stack.empty()) {
        Node* current = stack.top(); stack.pop();
        std::cout << node->value << std::endl;

        // Add children to stack such that left is processed before right.
        if (current->right) {
            stack.push(current->right);
        }
        if (current->left) {
            stack.push(current->left);
        }
    }
}
```
